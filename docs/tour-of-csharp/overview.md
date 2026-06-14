# C# là gì? Tổng quan cho người mới bắt đầu

C# (đọc là "C-sharp") là một ngôn ngữ lập trình phổ biến, được dùng để tạo ra đủ loại dự án trên nhiều nền tảng khác nhau. Bài viết này giới thiệu những ý chính để bạn hiểu C# là gì và có thể làm được những gì.

> **Mẹo nhỏ:**
> - **Chưa bao giờ lập trình trước đây?** Hãy lướt qua bài này để biết C# là gì, rồi bắt đầu [hướng dẫn cho người mới](tutorials/) để tập viết code thử.
> - **Biết Java, JavaScript hoặc Python?** Đọc thêm mẹo dành riêng cho nhà phát triển [Java](tips-for-java-developers), [JavaScript](tips-for-javascript-developers) hoặc [Python](tips-for-python-developers) cùng với bài này.
> - **Đã có kinh nghiệm nhưng mới học C#?** Bài này nói về những điểm đặc biệt của C#. Xem [Bạn có thể xây dựng gì với C#](what-you-can-build) để tìm việc phù hợp với mục tiêu của bạn.

C# là ngôn ngữ dùng nhiều nhất cho nền tảng **.NET** -- một bộ công cụ phát triển miễn phí, mã nguồn mở, chạy được trên nhiều hệ điều hành. **.NET** là một **framework** (khung lập trình) cung cấp môi trường để chạy và phát triển ứng dụng, gồm cả **runtime** (phần mềm nền -- chịu trách nhiệm thực thi chương trình) và **thư viện** (library) -- những đoạn code viết sẵn giúp bạn không phải "phát minh lại bánh xe". Chương trình C# có thể chạy trên nhiều loại thiết bị khác nhau, từ thiết bị nhỏ trong nhà thông minh (IoT - Internet of Things, mạng lưới các thiết bị vật lý kết nối Internet) đến máy chủ trên đám mây (cloud -- hệ thống máy chủ từ xa cho phép lưu trữ và xử lý dữ liệu qua Internet). Bạn có thể viết ứng dụng cho điện thoại, máy tính để bàn, máy tính xách tay và máy chủ. Xem [Bạn có thể xây dựng gì với C#](what-you-can-build) để biết thêm về các loại ứng dụng.

C# là ngôn ngữ đa năng, giúp bạn viết code nhanh và hiệu quả. Nó có nhiều thư viện hỗ trợ sẵn và rất nhiều [loại dự án](../../standard/glossary#workload) (**workload** = khối lượng công việc, ở đây chỉ các loại dự án/dạng ứng dụng khác nhau) khác nhau. C# được xây dựng trên tư tưởng **lập trình hướng đối tượng** (object-oriented programming - OOP: phương pháp tổ chức code xoay quanh các "đối tượng" có dữ liệu và hành vi), nhưng cũng kết hợp cả những ý tưởng từ **lập trình hàm** (functional programming: phong cách lập trình xử lý dữ liệu qua các hàm thuần túy, tránh thay đổi trạng thái). C# còn có những tính năng cấp thấp (low-level: cho phép can thiệp sâu vào bộ nhớ và phần cứng) giúp bạn viết code nhanh mà không cần dùng những kỹ thuật nguy hiểm. **Runtime** (phần mềm nền) và thư viện của .NET là những thành phần giúp chương trình C# của bạn chạy được -- phần lớn chúng đều được viết bằng chính C#.

C# thuộc "đại gia đình" ngôn ngữ họ C. [Cách viết câu lệnh trong C#](../language-reference/keywords/) sẽ quen thuộc nếu bạn đã từng dùng C, C++, JavaScript, TypeScript hoặc Java. Giống C và C++, bạn dùng **dấu chấm phẩy** (`;`) để kết thúc một câu lệnh. C# **phân biệt chữ hoa và chữ thường** (case-sensitive), nghĩa là `Hello` và `hello` là hai tên khác nhau. C# dùng **dấu ngoặc nhọn** `{` và `}` để bao khối lệnh (block), các câu lệnh điều khiển như `if`, `else`, `switch`, và các **vòng lặp** (loop) như `for` và `while`. C# cũng có câu lệnh `foreach` để duyệt qua mọi loại **tập hợp** (collection -- cấu trúc dữ liệu chứa nhiều phần tử, như danh sách, mảng).

---

## Xin chào thế giới (Hello World)

Chương trình "Hello, World" là cách truyền thống để bắt đầu học một ngôn ngữ mới. Dưới đây là chương trình Hello World trong C#:

```csharp
// Dòng này in ra "Hello, World"
Console.WriteLine("Hello, World");
```

Dòng bắt đầu bằng `//` là **chú thích một dòng** (single line comment). C# cũng có **chú thích nhiều dòng** (multi-line comment), bắt đầu bằng `/*` và kết thúc bằng `*/`. Chú thích là phần văn bản bị trình biên dịch bỏ qua, dùng để ghi chú giải thích cho người đọc code. Phương thức `WriteLine` (write line = viết một dòng) của lớp `Console` (console = bảng điều khiển, ở đây là cửa sổ dòng lệnh) -- nằm trong **namespace** `System` (namespace = không gian tên, cách nhóm các lớp liên quan lại với nhau) -- giúp chương trình in ra màn hình. **Thư viện chuẩn** (standard library) là bộ code viết sẵn đi kèm với .NET, cung cấp sẵn lớp này -- bạn không cần làm thêm gì cả.

Nếu bạn viết chương trình theo kiểu cũ hơn, bạn sẽ thấy nó dài hơn một chút. Trình biên dịch tự động hiểu cả hai kiểu viết:

```csharp
using System;

namespace TourOfCsharp;

class Program
{
    static void Main()
    {
        // Dòng này in ra "Hello, World"
        Console.WriteLine("Hello, World");
    }
}
```

Chương trình "Hello, World" phía trên bắt đầu bằng `using System`. Dòng `using` (using = sử dụng) giống như "mở cửa" một **namespace** (không gian tên), giúp bạn dùng các lớp trong namespace đó mà không cần viết tên đầy đủ. Ví dụ, nhờ có `using System`, bạn có thể viết `Console.WriteLine` thay vì phải viết `System.Console.WriteLine`. `Console` là tên lớp (class), `WriteLine` là tên phương thức (method), dấu `.` dùng để truy cập thành phần bên trong một lớp hoặc namespace.

> **Lưu ý:** Ở phiên bản cũ hơn, chương trình khai báo lớp `Program` với một **phương thức** (method) tên là `Main`. Phương thức `Main` là **điểm vào** (entry point) -- nơi chương trình bắt đầu chạy. **Phương thức** (method) là một khối code thực hiện một hành động cụ thể, có thể nhận đầu vào (tham số) và trả về kết quả. Kiểu viết mới gọi là **top-level statements** (câu lệnh cấp cao nhất -- không cần bọc trong lớp hay phương thức) đơn giản hơn và được khuyến khích cho người mới.

---

## Ứng dụng một file (File-based apps)

C# là ngôn ngữ **biên dịch** (compiled language). Nói nôm na, bạn viết code bằng chữ, rồi dùng **trình biên dịch** (compiler -- phần mềm chuyển đổi mã nguồn thành mã máy) để chuyển nó thành file mà máy tính có thể chạy được. Bạn dùng lệnh [`dotnet build`](../../core/tools/dotnet-build) (build = xây dựng, biên dịch dự án) để biên dịch và [`dotnet run`](../../core/tools/dotnet-run) để chạy chương trình.

Từ C# 14 và .NET 10 trở đi, bạn có thể tạo **ứng dụng một file** (single-file app) -- chỉ cần một file `*.cs` (`.cs` là phần mở rộng của file code C#) duy nhất là chạy được. Ví dụ, lưu code sau vào file `hello-world.cs` và chạy bằng `dotnet run hello-world.cs`:

```csharp
#!/usr/bin/env dotnet

Console.WriteLine("Hello, World!");
```

Dòng `#!` ở đầu (gọi là **shebang** -- một quy ước trên hệ thống Unix/Linux, cho hệ điều hành biết dùng chương trình nào để chạy file này) dành cho hệ điều hành Unix/Linux, giúp bạn chạy trực tiếp file C# như một **script** (tệp kịch bản -- file code được thực thi trực tiếp mà không cần biên dịch thủ công). Kiểu viết này rất tiện cho những tiện ích nhỏ, **nguyên mẫu** (prototype -- bản thử nghiệm nhanh để kiểm tra ý tưởng) hoặc thử nghiệm nhanh.

---

## Những tính năng quen thuộc trong C#

C# dễ học cho người mới nhưng vẫn đủ mạnh cho người có kinh nghiệm.

### Tự động dọn dẹp bộ nhớ (Garbage Collection)

Ứng dụng C# được hưởng lợi từ cơ chế **tự động dọn rác** (garbage collection - GC: runtime tự động giải phóng bộ nhớ của các đối tượng không còn được dùng đến, bạn không cần phải tự quản lý bộ nhớ như trong C/C++). Ngoài ra, **.NET SDK** (SDK = Software Development Kit, Bộ công cụ phát triển phần mềm) cung cấp sẵn [thư viện runtime](../../standard/runtime-libraries-overview) rất phong phú. Có những **thư viện độc lập với nền tảng** (platform-independent -- chạy được trên mọi hệ điều hành) như xử lý file, toán học, tập hợp dữ liệu, và những thư viện dành riêng cho từng [loại dự án](what-you-can-build) (web, điện thoại, desktop). Bạn cũng có thể tìm thêm thư viện mã nguồn mở (open source) trên [NuGet](https://nuget.org) -- kho thư viện chính thức của .NET.

### Kiểu dữ liệu cố định (Strongly typed)

C# là ngôn ngữ **kiểu dữ liệu chặt chẽ** (strongly typed). Nghĩa là mỗi **biến** (variable -- "hộp chứa" dùng để lưu trữ dữ liệu) bạn khai báo đều có một **kiểu dữ liệu** (data type) cụ thể, được **trình biên dịch** (compiler) kiểm tra trước khi chạy. Điều này giúp bạn phát hiện lỗi sớm, khi đang viết code chứ không phải lúc đang chạy (runtime). Ví dụ, nếu bạn khai báo biến là `int` (số nguyên) mà lại gán chữ cho nó, trình biên dịch sẽ báo lỗi ngay lập tức.

[Các kiểu dữ liệu cơ bản](../fundamentals/types/) được xây dựng sẵn trong ngôn ngữ:

- **Kiểu giá trị (value types)**: dữ liệu được lưu **trực tiếp** trong bộ nhớ. Gồm: `int` (số nguyên như 5, -100), `double` (số thực như 3.14), `char` (ký tự như `'A'`), `struct` (cấu trúc do bạn tự định nghĩa),...
- **Kiểu tham chiếu (reference types)**: biến chỉ lưu **địa chỉ** (tham chiếu) đến vùng nhớ chứa dữ liệu thực sự. Gồm: `string` (chuỗi văn bản), mảng (`array` -- dãy các phần tử cùng kiểu), `class` (lớp do bạn tự định nghĩa),...

Bạn cũng có thể tự tạo kiểu riêng:
- `struct` cho kiểu giá trị, phù hợp với dữ liệu nhỏ, đơn giản.
- `class` cho kiểu tham chiếu, hỗ trợ **lập trình hướng đối tượng** (OOP).
- Thêm `record` vào `struct` hoặc `class` để trình biên dịch tự động tạo mã so sánh (so sánh hai đối tượng dựa trên giá trị, không phải địa chỉ vùng nhớ).
- `interface` (giao diện) định nghĩa một "hợp đồng": những thành phần mà kiểu triển khai (implement) phải có.

Bạn còn có thể định nghĩa **kiểu generic** (generic type) và **phương thức generic** (generic method). [Generics](../fundamentals/types/generics) giống như một khuôn mẫu -- bạn dùng **tham số kiểu** (type parameters) để tạo ra code có thể làm việc với nhiều kiểu dữ liệu khác nhau. Ví dụ: `List<T>` có thể là `List<int>` (danh sách số nguyên) hoặc `List<string>` (danh sách chuỗi) tuỳ theo kiểu bạn truyền vào.

### Phương thức, Thuộc tính và Sự kiện

Khi viết code, bạn định nghĩa các **phương thức** (methods) bên trong `struct` và `class`. Phương thức là những hành động mà kiểu dữ liệu có thể thực hiện. Bạn có thể **nạp chồng** (overload) phương thức -- đặt tên giống nhau nhưng **tham số** (parameters -- đầu vào) khác nhau, trình biên dịch sẽ tự động chọn đúng phương thức dựa trên tham số bạn truyền vào. Phương thức có thể **trả về** (return) một giá trị hoặc không (dùng `void`).

Ngoài phương thức, kiểu C# còn có **thuộc tính** (properties) -- giống như biến nhưng được đọc/ghi thông qua các hàm gọi là **accessor** (bộ truy cập: `get` để đọc, `set` để ghi). Kiểu C# cũng có thể định nghĩa **sự kiện** (events), cho phép một kiểu "thông báo" cho những nơi khác biết có việc quan trọng xảy ra (ví dụ: nút button báo "tôi bị click").

C# hỗ trợ các kỹ thuật hướng đối tượng như **kế thừa** (inheritance -- một class có thể kế thừa dữ liệu và hành vi từ class khác) và **đa hình** (polymorphism -- cùng một phương thức nhưng có hành vi khác nhau tuỳ theo đối tượng) cho kiểu `class`.

### Xử lý lỗi (Exception)

Ứng dụng C# dùng **ngoại lệ** (exceptions) để báo cáo và xử lý lỗi -- bạn sẽ thấy quen nếu đã từng dùng C++ hoặc Java. **Ngoại lệ** (exception) là một sự kiện bất thường xảy ra trong quá trình chạy chương trình (ví dụ: chia cho 0, không tìm thấy file). Code của bạn sẽ **ném** (throw) một ngoại lệ khi gặp sự cố. Code ở nơi khác có thể **bắt** (catch) ngoại lệ đó bằng khối `try`-`catch`:

```csharp
try
{
    // Code có thể gây lỗi
}
catch (Exception ex)
{
    // Xử lý khi có lỗi xảy ra
}
```

- `try` (thử) bao quanh đoạn code có thể phát sinh lỗi.
- `catch` (bắt) xử lý lỗi khi nó xảy ra, giúp chương trình không bị treo.
- `Exception` là lớp cơ sở (base class) cho mọi ngoại lệ trong C#.
- `ex` là biến chứa thông tin chi tiết về lỗi.

> **Mẹo:** Để tìm hiểu thêm về kiểu dữ liệu, phương thức và ngoại lệ, hãy xem phần [C# cơ bản](../fundamentals/program-structure/). Phần này gồm có [hệ thống kiểu](../fundamentals/types/), [lập trình hướng đối tượng](../fundamentals/object-oriented/) và [xử lý ngoại lệ](../fundamentals/exceptions/) một cách chi tiết.

---

## Những tính năng đặc biệt của C#

Một số tính năng dưới đây có thể mới lạ nhưng rất hữu ích.

### So khớp mẫu (Pattern matching)

C# cung cấp [so khớp mẫu](../fundamentals/functional/pattern-matching) (pattern matching). Nó cho phép bạn kiểm tra dữ liệu và đưa ra quyết định dựa trên đặc điểm của dữ liệu đó. Pattern matching giúp viết code điều khiển luồng xử lý một cách dễ đọc. Đoạn code dưới đây cho thấy cách dùng pattern matching với **switch expression** (biểu thức switch -- một dạng rẽ nhánh rút gọn, kiểm tra giá trị và trả về kết quả trực tiếp) để viết hàm phép toán *and* (và), *or* (hoặc) và *xor* (hoặc loại trừ -- chỉ đúng khi hai giá trị khác nhau):

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

- `(left, right) switch` -- tạo một **tuple** (bộ) từ `left` và `right`, rồi so khớp với các mẫu bên trong.
- `=>` -- "thì trả về". Mỗi dòng là một mẫu (pattern) và kết quả tương ứng.

Bạn có thể rút gọn bằng cách dùng `_` (dấu gạch dưới, underscore) làm **ký tự đại diện** (catchall / discard -- khớp với mọi giá trị, không cần quan tâm nó là gì):

```csharp
public static bool ReducedAnd(bool left, bool right) =>
    (left, right) switch
    {
        (true, true) => true,
        (_, _) => false,
    };
```

### Tuple (Bộ) -- gom nhiều giá trị thành một

**Tuple** (đọc là "túp-pơ", bộ) là một cấu trúc dữ liệu nhẹ, cho phép bạn gom nhiều giá trị lại với nhau mà không cần định nghĩa kiểu riêng. Bạn đặt các giá trị trong dấu `(` và `)` và phân cách bằng dấu phẩy. Ví dụ `(left, right)` là một tuple có hai giá trị kiểu bool.

```csharp
var point = (x: 10, y: 20);
Console.WriteLine(point.x); // In ra: 10
```

- `var` (variable) -- từ khóa bảo trình biên dịch tự suy ra kiểu dữ liệu dựa trên giá trị gán.
- `(x: 10, y: 20)` -- tuple có tên cho từng thành phần (`x` và `y`). Bạn có thể truy cập bằng `point.x` hoặc `point.y`.
- Tuple rất tiện khi bạn muốn trả về nhiều giá trị từ một phương thức mà không cần tạo class riêng.

### Cách viết ngắn gọn cho collection (Collection expressions)

**Collection expressions** (biểu thức tập hợp) -- [cú pháp](../language-reference/operators/collection-expressions) cho phép bạn tạo **collection** (tập hợp dữ liệu, như danh sách hoặc mảng) bằng cách đặt các giá trị trong `[` và `]`:

```csharp
int[] numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
List<string> names = ["Alice", "Bob", "Charlie", "David"];

IEnumerable<int> moreNumbers = [.. numbers, 11, 12, 13];
IEnumerable<string> empty = [];
```

- `int[]` -- mảng (array) số nguyên. Mảng có kích thước cố định.
- `List<string>` -- danh sách (list) các chuỗi, có thể thay đổi kích thước.
- `IEnumerable<int>` -- một **giao diện** (interface) đại diện cho bất kỳ collection nào có thể duyệt qua (dùng `foreach`). Nó là kiểu trừu tượng nhất.
- `[.. numbers, 11, 12, 13]` -- dùng `..` (spread element) để "trải" tất cả phần tử của `numbers` vào collection mới, rồi thêm 11, 12, 13.
- `[]` -- collection rỗng (không có phần tử nào).

### Chỉ số và Khoảng (Index & Range)

**Index** (chỉ số) và **Range** (khoảng) là cú pháp giúp truy cập phần tử trong collection linh hoạt hơn. Bạn có thể dùng `^` để lấy phần tử từ cuối collection, và `..` để lấy một khoảng phần tử:

```csharp
string second = names[1];    // Index bắt đầu từ 0
string last = names[^1];     // ^1 là phần tử cuối cùng
int[] smallNumbers = numbers[0..5]; // các phần tử từ index 0 đến 4
```

- `names[1]` -- lấy phần tử ở **index** (chỉ số, vị trí) thứ 1. Index trong C# bắt đầu từ 0, nên `[0]` là phần tử đầu tiên, `[1]` là phần tử thứ hai.
- `^` (dấu mũ) -- **toán tử index từ cuối** (index from end). `^1` là phần tử cuối cùng, `^2` là phần tử kế cuối, `^3` là phần tử thứ ba từ cuối,... Cách này tiện hơn đếm ngược: `names[names.Length - 1]`.
- `..` (hai dấu chấm) -- **toán tử range** (khoảng). `0..5` lấy các phần tử từ index 0 đến index 4 (không bao gồm 5).
- Bạn cũng có thể kết hợp: `numbers[^3..]` -- lấy 3 phần tử cuối cùng.

Xem thêm bài viết [Khám phá index và range](../tutorials/ranges-indexes).

### Truy vấn dữ liệu với LINQ

**LINQ** (Language-Integrated Query -- Ngôn ngữ truy vấn tích hợp) là một trong những tính năng mạnh nhất của C#. Nó cho phép bạn dùng cùng một cách viết (cú pháp) để truy vấn dữ liệu từ nhiều nguồn khác nhau: bộ nhớ (mảng, danh sách), XML, cơ sở dữ liệu (SQL), hoặc API đám mây. Bạn chỉ cần học một bộ cú pháp là có thể xử lý dữ liệu ở mọi nơi.

Truy vấn sau tìm tất cả sinh viên có điểm trung bình (**GPA** -- Grade Point Average, điểm trung bình tích lũy) lớn hơn 3.5:

```csharp
var honorRoll = from student in Students
                where student.GPA > 3.5
                select student;
```

- `from student in Students` -- duyệt qua từng `student` trong tập `Students`.
- `where student.GPA > 3.5` -- lọc chỉ giữ lại sinh viên có GPA > 3.5.
- `select student` -- trả về kết quả là các sinh viên đã lọc.
- `var` -- trình biên dịch tự suy ra kiểu dữ liệu trả về (ở đây là một collection các Student).

LINQ có thể hoạt động trên bộ nhớ (**LINQ to Objects**), cơ sở dữ liệu (**LINQ to SQL**, **Entity Framework**), hoặc bất kỳ nguồn dữ liệu nào có hỗ trợ **IEnumerable** hoặc **IQueryable**.

### Lập trình bất đồng bộ (async / await)

**Bất đồng bộ** (asynchronous -- viết tắt là async) là kỹ thuật cho phép chương trình tiếp tục làm việc khác trong khi chờ một tác vụ tốn thời gian hoàn thành (ví dụ: tải file từ Internet, đọc file từ ổ cứng), thay vì phải đứng chờ và "đơ" (block). [Mô hình lập trình bất đồng bộ](../asynchronous-programming/) trong C# cho phép bạn viết code trông như chạy tuần tự (dễ đọc) nhưng thật ra chạy bất đồng bộ bên dưới. Bạn dùng từ khóa `async` để đánh dấu **phương thức** (method) là bất đồng bộ, và `await` (chờ đợi) để chờ một **tác vụ** (task -- đại diện cho công việc đang chạy) hoàn thành.

Ví dụ sau gửi một yêu cầu web bất đồng bộ. Code chờ đến khi tải về xong rồi mới trả về độ dài:

```csharp
public static async Task<int> GetPageLengthAsync(string endpoint)
{
    var client = new HttpClient();
    var uri = new Uri(endpoint);
    byte[] content = await client.GetByteArrayAsync(uri);
    return content.Length;
}
```

- `async Task<int>` -- phương thức này chạy bất đồng bộ và trả về một số nguyên (`int`) bên trong `Task`. `Task<T>` là "lời hứa" sẽ có kết quả kiểu `T` trong tương lai.
- `await client.GetByteArrayAsync(uri)` -- gửi yêu cầu web và... chờ (nhưng không block -- thread vẫn có thể làm việc khác). Khi có kết quả, chương trình tiếp tục chạy dòng tiếp theo.
- `HttpClient` -- lớp thư viện chuẩn dùng để gửi và nhận dữ liệu qua HTTP (giao thức web).

C# cũng có `await foreach` để duyệt qua collection được tải bất đồng bộ từng phần, rất hữu ích khi làm việc với **API phân trang** (pagination -- dữ liệu được chia thành nhiều trang nhỏ, mỗi lần chỉ tải một trang):

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

- `IAsyncEnumerable<int>` -- collection có thể duyệt bất đồng bộ, trả về từng số nguyên một.
- `yield return` -- trả về một phần tử và tạm dừng phương thức, lần sau gọi sẽ tiếp tục từ chỗ dừng.
- `yield break` -- kết thúc việc trả về (không còn phần tử nào nữa).

Người gọi có thể duyệt bằng `await foreach`:

```csharp
await foreach (var number in ReadSequence())
{
    Console.WriteLine(number);
}
```

Không có `await` ở đây, `foreach` sẽ không biết rằng mỗi lần lấy phần tử tiếp theo có thể phải chờ tải dữ liệu từ mạng.

### Công cụ phát triển (IDE)

**IDE** (Integrated Development Environment -- Môi trường phát triển tích hợp) là phần mềm giúp bạn viết code hiệu quả hơn. Bạn có thể dùng [Visual Studio](https://visualstudio.microsoft.com/vs) hoặc [Visual Studio Code](https://code.visualstudio.com) với [C# DevKit](https://code.visualstudio.com/docs/csharp/get-started) để viết code C#. Các công cụ này giúp bạn:
- Viết code nhanh hơn nhờ **IntelliSense** (gợi ý code khi gõ).
- **Phát hiện lỗi** (syntax highlighting, error squiggles) ngay khi gõ, không cần đợi biên dịch.
- **Gỡ lỗi** (debug -- chạy từng bước để tìm lỗi) dễ dàng với breakpoint (điểm dừng) và watch (xem giá trị biến).

> **Mẹo:** Để tìm hiểu thêm về pattern matching, LINQ và lập trình bất đồng bộ, hãy xem các phần [kỹ thuật hàm](../fundamentals/functional/pattern-matching), [tổng quan LINQ](../linq/) và [lập trình bất đồng bộ](../asynchronous-programming/).

---

## Bước tiếp theo

Bài viết này đã cho bạn một cái nhìn nhanh về C#. Dưới đây là những hướng đi tiếp theo, tùy theo trình độ của bạn:

- **Bắt đầu viết code**: Làm qua [hướng dẫn cho người mới bắt đầu](tutorials/) để học C# từng bước một với các bài tập tương tác.
- **Đi sâu hơn**: Xem phần [C# cơ bản](../fundamentals/program-structure/) (**fundamentals** -- kiến thức nền tảng) để biết chi tiết về **hệ thống kiểu** (type system), **lập trình hướng đối tượng** (OOP) và **xử lý lỗi** (error handling).
- **Xây dựng ứng dụng**: Khám phá [bạn có thể xây dựng gì với C#](what-you-can-build) để tìm ý tưởng và **workload** (dạng dự án) phù hợp với mục tiêu của bạn.
- **Đến từ ngôn ngữ khác?** Đọc hướng dẫn dành riêng cho nhà phát triển [Java](tips-for-java-developers), [JavaScript](tips-for-javascript-developers) hoặc [Python](tips-for-python-developers) để thấy sự khác biệt và điểm tương đồng.
- **Xây dựng ứng dụng một file**: Tìm hiểu cách [xây dựng file-based apps](../fundamentals/tutorials/file-based-programs) (**ứng dụng dạng tệp** -- chỉ cần một file `.cs` duy nhất) cho các chương trình nhỏ, thử nghiệm nhanh và **nguyên mẫu** (prototype).
