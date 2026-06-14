---
title: Hướng dẫn tương tác
description: Học C# bằng GitHub Codespaces và bắt đầu với môi trường phát triển của riêng bạn.
ms.date: 02/09/2026
---
# Giới thiệu về C\#

Chào mừng bạn đến với loạt bài hướng dẫn giới thiệu về C#. Những bài học này bắt đầu với mã tương tác mà bạn có thể chạy trong GitHub Codespaces. Bạn có thể học những kiến thức cơ bản về C# từ [chuỗi video C# for Beginners](https://aka.ms/dotnet/beginnervideos/youtube/csharp) trước khi bắt đầu các bài học tương tác này.

> [!TIP]
> **Mới học lập trình?** Hãy bắt đầu với bài 1 ([Hello world](hello-world.md)) và làm lần lượt từng bài học.
>
> **Đã biết ngôn ngữ khác?** Bạn có thể lướt qua bài 1–2 và bắt đầu với [Tuple và kiểu dữ liệu](tuples-and-types.md) để học những khái niệm có thể còn mới.

Tất cả các bài hướng dẫn đều sử dụng ứng dụng dạng file. Bạn có thể dùng [GitHub Codespace](https://github.com/dotnet/tutorial-codespace) của chúng tôi, hoặc cài đặt [.NET SDK](../../../core/install/index.yml), và bạn đã sẵn sàng để bắt đầu.

<!--markdownlint-disable-next-line MD034 -->
> [!VIDEO https://www.youtube.com/embed/9THmGiSPjBQ?si=3kUKFtOMLpEzeq7J]

Những bài học đầu tiên giải thích các khái niệm C# bằng cách sử dụng những đoạn mã nhỏ. Bạn sẽ học syntax (cú pháp) cơ bản của C# và cách làm việc với các kiểu dữ liệu (data types) như chuỗi (string), số (number) và Boolean. Tất cả đều mang tính tương tác, và bạn sẽ viết cũng như chạy mã chỉ trong vài phút. Những bài học đầu tiên này không yêu cầu bạn phải có kiến thức lập trình hay ngôn ngữ C# từ trước. Mỗi bài học đều được xây dựng dựa trên bài trước đó, vì vậy bạn nên làm theo thứ tự. Tuy nhiên, nếu bạn đã có kinh nghiệm lập trình, bạn có thể bỏ qua hoặc lướt nhanh các bài đầu và bắt đầu với bất kỳ khái niệm mới nào.

Để sử dụng GitHub Codespaces, bạn cần tạo một tài khoản [GitHub](https://github.com) miễn phí.

## Hello world

Trong bài hướng dẫn [Hello world](hello-world.md), bạn sẽ tạo chương trình C# cơ bản nhất. Bạn sẽ khám phá kiểu `string` (chuỗi) và cách làm việc với văn bản.

## Numbers in C\#

Trong bài hướng dẫn [Số trong C#](numbers-in-csharp.md), bạn sẽ học cách máy tính lưu trữ số và cách thực hiện tính toán với các kiểu số khác nhau. Bạn sẽ học những kiến thức cơ bản về làm tròn số và cách thực hiện các phép tính toán học bằng C#.

## Tuples and types

Trong bài hướng dẫn [Tuple và kiểu dữ liệu](tuples-and-types.md), bạn sẽ học cách tạo kiểu dữ liệu (types) trong C#. Bạn có thể tạo các kiểu *tuple*, *records (bản ghi)*, *struct (cấu trúc)* và *class (lớp)*. Khả năng của các kiểu dữ liệu khác nhau này phản ánh các mục đích sử dụng khác nhau của chúng.

## Branches and loops

Bài hướng dẫn [Rẽ nhánh và vòng lặp](branches-and-loops.md) dạy bạn những kiến thức cơ bản về cách chọn các nhánh thực thi mã khác nhau dựa trên giá trị được lưu trong các variable (biến). Bạn sẽ học những điều cơ bản về luồng điều khiển (control flow) - nền tảng cho cách chương trình đưa ra quyết định và chọn các hành động khác nhau.

## List collection

Bài học [Bộ sưu tập danh sách](list-collection.md) sẽ giới thiệu cho bạn về kiểu bộ sưu tập List dùng để lưu trữ các chuỗi dữ liệu. Bạn sẽ học cách thêm, xoá, tìm kiếm và sắp xếp danh sách. Bạn cũng sẽ khám phá các loại danh sách khác nhau.

## Pattern matching

Bài học [So khớp mẫu](pattern-matching.md) cung cấp phần giới thiệu về *pattern matching (so khớp mẫu)*. Pattern matching cho phép bạn so sánh một expression (biểu thức) với một pattern (mẫu). Kết quả so khớp sẽ quyết định logic chương trình nào được thực thi. Pattern có thể so sánh kiểu dữ liệu, thuộc tính (properties) của một kiểu, hoặc nội dung của một danh sách. Bạn có thể kết hợp nhiều pattern bằng cách sử dụng logic `and`, `or` và `not`. Pattern cung cấp một vốn từ vựng phong phú để kiểm tra dữ liệu và đưa ra quyết định trong chương trình dựa trên kết quả kiểm tra đó.

## Tiếp theo là gì?

Sau khi hoàn thành các bài hướng dẫn này, hãy tiếp tục hành trình học tập của bạn:

- [Xây dựng ứng dụng dạng file](../../fundamentals/tutorials/file-based-programs.md): Tìm hiểu cách tạo và chạy chương trình C# một file từ dòng lệnh.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md): Khám phá các loại ứng dụng bạn có thể tạo bằng C#.
- [Hệ thống kiểu dữ liệu C#](../../fundamentals/types/index.md): Đi sâu hơn vào kiểu giá trị (value types), kiểu tham chiếu (reference types), generics (kiểu tổng quát), v.v.
- [Kiến thức nền tảng C#](../../fundamentals/program-structure/index.md): Tìm hiểu về cấu trúc chương trình, lập trình hướng đối tượng và xử lý lỗi.
