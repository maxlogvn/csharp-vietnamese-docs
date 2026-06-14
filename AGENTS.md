# Hướng dẫn dịch tài liệu C# từ tiếng Anh sang tiếng Việt

## Mục tiêu

Dịch tài liệu trong thư mục `docs/en/` sang `docs/vi/` với phong cách thân thiện, dễ hiểu dành cho lập trình viên mới học C#. Nội dung phải chi tiết, rõ ràng và không lạm dụng thuật ngữ chuyên ngành.

## Nguyên tắc dịch

### 1. Ngôn ngữ tự nhiên, gần gũi

- Viết bằng tiếng Việt với giọng văn tự nhiên như đang trò chuyện, hướng dẫn người mới học.
- Hạn chế câu dài, cấu trúc phức tạp. Nếu câu tiếng Anh quá dài, hãy chia nhỏ thành nhiều câu tiếng Việt.
- Không bê nguyên cấu trúc câu tiếng Anh vào tiếng Việt (tránh "Anh ngữ").

### 2. Xử lý thuật ngữ chuyên ngành

- **Ưu tiên thuật ngữ tiếng Việt quen thuộc:** nếu từ đó đã được dùng nhiều và dễ hiểu, hãy dịch thẳng sang tiếng Việt.
- **Khi dịch thuật ngữ:** viết theo cú pháp `thuật ngữ gốc (bản dịch)`, ví dụ:
  - `delegate` -> `delegate (uỷ quyền)`
  - `method` -> `method (phương thức)`
  - `class` -> `class (lớp)`
  - `variable` -> `variable (biến)`
  - `array` -> `array (mảng)`
  - `object` -> `object (đối tượng)`
- **Giữ nguyên thuật ngữ gốc nếu cần:** một số từ phổ biến đến mức ai cũng biết như `class`, `method`, `variable`, `enum`, `interface`, `object` thì có thể giữ nguyên tiếng Anh và thêm bản dịch trong ngoặc ở lần xuất hiện đầu tiên của mỗi file. Các lần sau chỉ cần dùng tiếng Anh.
- **Luôn có ví dụ minh hoạ** kèm theo khi giới thiệu khái niệm mới.

Ví dụ:
> **Delegate (uỷ quyền)** là một kiểu dữ liệu cho phép bạn tham chiếu tới một method (phương thức). Giống như bạn đưa một số điện thoại cho người bạn và bảo "khi cần thì gọi số này" - delegate cũng vậy, nó cho bạn biết cần gọi method nào.

> **Numbers in C# (Số trong C#)** - C# hỗ trợ nhiều loại số khác nhau: `int` cho số nguyên (ví dụ: 5, -3, 100), `double` cho số thập phân (ví dụ: 3.14, -0.5), `decimal` cho tiền tệ và tính toán chính xác cao.

### 3. Giữ nguyên mã nguồn (code)

- **KHÔNG dịch** mã C#. Tất cả code block giữ nguyên.
- **KHÔNG dịch** tên biến, tên method, tên class trong code.
- **Có thể thêm comment tiếng Việt bên cạnh** nếu cần giải thích thêm, nhưng không thay đổi code gốc.

### 4. Xử lý cấu trúc và cú pháp đặc thù

- Giữ nguyên heading levels (`#`, `##`, `###`).
- **Liên kết (links) phải có hiển thị thuần tiếng Việt:** không kèm tiếng Anh trong ngoặc `(...)`. Chỉ giữ lại tên riêng, từ viết tắt (LINQ, WPF) và keyword code (`ref`, `in`, `out`). Ví dụ:
  - `[Tổng quan về C#](overview.md)` thay vì `[C# Overview (Tổng quan về C#)](overview.md)`
  - `[chuỗi](hello-world.md)` thay vì `[strings (chuỗi)](hello-world.md)`
- Giữ nguyên images, `> [!NOTE]`, `> [!IMPORTANT]` và front matter (phần `---` ở đầu file).
- **Chuyển `:::code` DocFX thành code block Markdown chuẩn:** đọc file nguồn được tham chiếu trong thuộc tính `source`, lấy nội dung tương ứng với `id` (nếu có), và đặt vào ```csharp.
- **Chuyển `<xref:...>` thành link Markdown chuẩn:** ví dụ `<xref:System.Object>` thành [`Object`](https://learn.microsoft.com/dotnet/api/system.object).
- Không xoá bất kỳ nội dung nào, chỉ dịch.
- Duy trì đúng thư mục tương ứng: `docs/en/code/abc.md` -> `docs/vi/code/abc.md`.

### 5. Chất lượng

- Kiểm tra lại bản dịch: đọc thử bằng tiếng Việt xem có trôi chảy, tự nhiên không.
- Kiểm tra chính tả và dấu câu tiếng Việt đầy đủ.
- Đảm bảo thông tin kỹ thuật không bị sai lệch.

## Quy trình dịch

**Mỗi lần chỉ được dịch MỘT file duy nhất.**

1. **Chọn file:** nhận chỉ định file cần dịch từ người dùng.
2. **Đọc file gốc:** đọc toàn bộ nội dung file gốc trong `docs/en/`.
3. **Xác định file đích:** kiểm tra file tương ứng trong `docs/vi/`. Nếu đã có, đọc nội dung hiện tại. Nếu chưa có, sẽ tạo mới.
4. **Kiểm tra thư mục:** đảm bảo thư mục cha của file đích đã tồn tại trong `docs/vi/`.
5. **Dịch:** thực hiện dịch toàn bộ file theo các nguyên tắc trên.
6. **Xác nhận với người dùng:** hiển thị thông báo "Da hoan thanh dich file: `path/to/file.md`." sau khi hoàn tất.
