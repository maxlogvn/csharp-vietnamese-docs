---
title: Bạn có thể xây dựng gì với C#
description: Khám phá các loại ứng dụng bạn có thể xây dựng với C#, bao gồm web, desktop, mobile, cloud, IoT, AI và game.
ms.date: 02/10/2026
ai-usage: ai-assisted
---

# Bạn có thể xây dựng gì với C\#

C# hỗ trợ rất nhiều loại ứng dụng khác nhau. Dù bạn muốn xây dựng phần mềm gì, thì khả năng cao là luôn có một [workload](../../standard/glossary.md#workload) (khối lượng công việc) dành cho nó. Bài viết này sẽ cung cấp cho bạn cái nhìn tổng quan về các loại ứng dụng phổ biến nhất, kèm theo các đường dẫn để bắt đầu với từng loại.

> [!TIP]
> **Mới học lập trình?** Đừng lo lắng về việc chọn workload ngay bây giờ. Trước hết hãy tập trung [học ngôn ngữ C#](tutorials/index.md). Bạn có thể khám phá các loại ứng dụng này sau khi đã quen với những kiến thức cơ bản.
>
> **Lập trình viên có kinh nghiệm?** Hãy nhảy thẳng tới workload phù hợp với mục tiêu của bạn. Mỗi phần đều có đường dẫn tới tài liệu và bài hướng dẫn bạn cần.

## AI và machine learning (học máy)

C# tích hợp với các công cụ AI và machine learning:

- **[Agent Framework](/agent-framework/overview/?pivots=programming-language-csharp)** - Xây dựng các agent (tác tử) và quy trình làm việc cho Azure, OpenAI, Anthropic, Ollama, v.v.
- **[Foundry Tools](/azure/ai-services/)** - Truy cập các khả năng AI có sẵn như thị giác máy tính, hiểu ngôn ngữ và nhận dạng giọng nói.
- **[ML.NET](../../machine-learning/index.yml)** - Xây dựng các mô hình machine learning tuỳ chỉnh bằng C# mà không cần chuyên môn sâu về ML.

Bắt đầu: [Hướng dẫn ML.NET](../../machine-learning/index.yml).

## Ứng dụng Web

Xây dựng ứng dụng web với [ASP.NET Core](/aspnet/core/), framework đa nền tảng để tạo các ứng dụng web và API hiện đại. Bạn có thể xây dựng:

- **Ứng dụng web kết xuất từ server (server-rendered)** sử dụng Razor Pages hoặc MVC.
- **Giao diện web tương tác** sử dụng [Blazor](/aspnet/core/blazor/), cho phép bạn viết logic phía client bằng C# thay vì JavaScript.
- **Web API** và [minimal API](/aspnet/core/fundamentals/minimal-apis/overview) cho các dịch vụ backend.

Bắt đầu: [Hướng dẫn ASP.NET Core](/aspnet/core/tutorials)

## Ứng dụng Desktop

Dùng C# để xây dựng ứng dụng desktop trên Windows và ứng dụng desktop đa nền tảng chạy trên cả Windows và macOS:

- **[.NET MAUI](/dotnet/maui/)** tạo ứng dụng desktop đa nền tảng chạy trên Windows, macOS, Android và iOS từ một codebase (cơ sở mã) duy nhất.
- **[Windows Presentation Foundation (WPF)](/dotnet/desktop/wpf/)** xây dựng ứng dụng desktop giàu tính năng chỉ dành cho Windows với đồ hoạ nâng cao và data binding (liên kết dữ liệu).
- **[Windows Forms](/dotnet/desktop/winforms/)** cung cấp cách thức đơn giản để tạo ứng dụng desktop chỉ dành cho Windows với trình thiết kế visual designer (trình thiết kế trực quan).

Bắt đầu: [Hướng dẫn .NET MAUI](/dotnet/maui/get-started/first-app).

## Ứng dụng Mobile

Xây dựng ứng dụng di động native (gốc) cho iOS và Android bằng [.NET MAUI](/dotnet/maui/). .NET MAUI cho phép bạn dùng chung code trên cả nền tảng di động và desktop, đồng thời vẫn truy cập được các API thiết bị gốc như camera, cảm biến, GPS, v.v.

Bắt đầu: [Xây dựng ứng dụng .NET MAUI đầu tiên của bạn](/dotnet/maui/get-started/first-app).

## Cloud và microservices

C# rất phù hợp để xây dựng các ứng dụng cloud-native (gốc điện toán đám mây) và microservices:

- **[Azure SDK for .NET](../../azure/sdk/azure-sdk-for-dotnet.md)** cung cấp các thư viện để làm việc với các dịch vụ Azure như lưu trữ, nhắn tin và cơ sở dữ liệu.
- **[Worker Services](../../core/extensions/workers.md)** cho phép bạn xây dựng các long-running background services (dịch vụ nền chạy lâu dài) trên cloud hoặc on-premises (tại chỗ).
- **[Aspire](https://aspire.dev)** giúp hợp lý hoá việc xây dựng, chạy, triển khai, gỡ lỗi và triển khai các ứng dụng phân tán.

Bắt đầu: [Bắt đầu với Azure và .NET](../../azure/index.yml).

## Game

C# là một trong những ngôn ngữ phổ biến nhất để phát triển game:

- **[Unity](https://docs.unity3d.com/Manual/index.html)** - Engine game được sử dụng rộng rãi nhất cho game 2D và 3D, sử dụng C# làm scripting language (ngôn ngữ kịch bản).
- **[MonoGame](https://docs.monogame.net/?page=main)** - Framework mã nguồn mở để tạo game đa nền tảng.
- **[CryEngine](https://docs.cryengine.com/display/CEPROG/C%23+Programming)** - Hỗ trợ C# cho việc viết kịch bản game.

Bạn cũng có thể sử dụng [Visual Studio để phát triển game](https://visualstudio.microsoft.com/vs/features/game-development/?utm_medium=microsoft&utm_source=learn.microsoft.com&utm_campaign=inline+link) với các engine này.

## Internet of Things (IoT)

Điều khiển thiết bị và đọc dữ liệu cảm biến bằng [thư viện IoT](../../iot/index.yml). Bạn có thể chạy ứng dụng C# trên các thiết bị như [Raspberry Pi](../../iot/quickstarts/sensehat.md) và các máy tính bảng đơn (single-board computer) khác để xây dựng các giải pháp IoT.

Bắt đầu: [Hướng dẫn IoT](../../iot/tutorials/blink-led.md)

## Các bước tiếp theo

Giờ bạn đã biết mình có thể xây dựng gì, hãy chọn bước tiếp theo:

- **Học ngôn ngữ**: Bắt đầu với [hướng dẫn C# cho người mới bắt đầu](tutorials/index.md) để học các kiến thức nền tảng về C#.
- **Khám phá C#**: Đọc [Tổng quan về C#](overview.md) để có cái nhìn tổng quát về các tính năng chính của ngôn ngữ.
- **Đào sâu kiến thức nền tảng**: Truy cập phần [Kiến thức nền tảng C#](../fundamentals/program-structure/index.md) để tìm hiểu sâu hơn về hệ thống kiểu (type system), lập trình hướng đối tượng (object-oriented programming), v.v.
- **Đến từ ngôn ngữ khác?** Xem lộ trình dành cho nhà phát triển [Java](tips-for-java-developers.md), [JavaScript/TypeScript](tips-for-javascript-developers.md) hoặc [Python](tips-for-python-developers.md).
