---
title: Những ứng dụng bạn có thể xây dựng với C#
description: Khám phá các loại ứng dụng bạn có thể xây dựng với C#, bao gồm ứng dụng web, desktop, di động, đám mây, IoT, AI và trò chơi.
ms.date: 02/10/2026
ai-usage: ai-assisted
---

# Những ứng dụng bạn có thể xây dựng với C\#

C# hỗ trợ rất nhiều loại ứng dụng khác nhau. Dù bạn muốn xây dựng loại phần mềm nào, cũng sẽ có một **workload** (khối lượng công việc -- ở đây chỉ "dạng dự án" hoặc "loại ứng dụng") phù hợp dành cho nó, được liệt kê trong [glossary (bảng thuật ngữ)](../../standard/glossary.md#workload). Mỗi workload đi kèm với các công cụ và thư viện riêng do .NET SDK cung cấp. Bài viết này sẽ cung cấp cho bạn cái nhìn tổng quan về những loại ứng dụng phổ biến nhất, kèm theo các đường dẫn để bạn bắt đầu với từng loại.

> [!TIP]
> **Mới học lập trình?** Đừng lo lắng về việc chọn **workload** ngay bây giờ. Hãy tập trung vào [học ngôn ngữ C#](tutorials/index.md) trước. Bạn có thể khám phá các loại ứng dụng này sau khi đã quen với những kiến thức cơ bản.
>
> **Đã có kinh nghiệm?** Hãy nhảy thẳng tới workload phù hợp với mục tiêu của bạn. Mỗi phần đều có các đường dẫn tới tài liệu và hướng dẫn bạn cần.

## AI và máy học

**AI** (Artificial Intelligence -- Trí tuệ nhân tạo) và **machine learning** (máy học -- một nhánh của AI, cho phép máy tính tự học từ dữ liệu thay vì được lập trình cứng nhắc). C# tích hợp với các công cụ AI và máy học:

- **[Agent Framework](/agent-framework/overview/?pivots=programming-language-csharp)** - Xây dựng các **tác nhân** (agent -- chương trình tự động thực hiện tác vụ thay cho con người) và **quy trình làm việc** (workflow) cho Azure, OpenAI, Anthropic, Ollama và nhiều nền tảng khác.
- **[Foundry Tools](/azure/ai-services/)** - Truy cập các khả năng AI có sẵn như **thị giác máy tính** (computer vision -- nhận diện hình ảnh), **hiểu ngôn ngữ** (ngôn ngữ tự nhiên -- NLP) và **nhận dạng giọng nói** (speech recognition).
- **[ML.NET](../../machine-learning/index.yml)** - Xây dựng các **mô hình máy học** (ML model -- chương trình đã được "huấn luyện" để nhận diện mẫu trong dữ liệu) tùy chỉnh trong C# mà không cần có chuyên môn sâu về ML.

Bắt đầu: [Hướng dẫn ML.NET](../../machine-learning/index.yml).

## Ứng dụng web

Xây dựng ứng dụng web với [ASP.NET Core](/aspnet/core/) - một **framework** (khung lập trình -- bộ thư viện và công cụ có sẵn giúp phát triển ứng dụng nhanh hơn) đa nền tảng (chạy được trên Windows, Linux, macOS) để tạo các ứng dụng web và API hiện đại. Bạn có thể xây dựng:

- **Ứng dụng web kết xuất từ máy chủ** (server-rendered -- máy chủ tạo ra HTML và gửi cho trình duyệt) bằng Razor Pages hoặc **MVC** (Model-View-Controller -- một mẫu kiến trúc phân chia code thành 3 phần: dữ liệu, giao diện và điều khiển).
- **Giao diện người dùng web tương tác** bằng [Blazor](/aspnet/core/blazor/), cho phép bạn viết **logic phía client** (client-side -- code chạy trên trình duyệt của người dùng) bằng C# thay vì JavaScript.
- **Web API** (Application Programming Interface -- giao diện lập trình ứng dụng, cho phép các ứng dụng khác giao tiếp với nhau qua HTTP) và **Minimal APIs** (API tối giản -- cách viết API đơn giản với ít code hơn) cho các **dịch vụ backend** (backend -- phần xử lý phía máy chủ).

Bắt đầu: [Hướng dẫn ASP.NET Core](/aspnet/core/tutorials).

## Ứng dụng desktop

**Desktop** (máy tính để bàn) -- ứng dụng chạy trực tiếp trên hệ điều hành của máy tính, có cửa sổ, nút bấm, menu,... Sử dụng C# để xây dựng ứng dụng desktop trên Windows, và ứng dụng desktop đa nền tảng (cross-platform -- chạy được trên nhiều hệ điều hành) chạy trên cả Windows và macOS:

- **[.NET MAUI](/dotnet/maui/)** (.NET Multi-platform App UI -- Giao diện ứng dụng đa nền tảng) cho phép tạo ứng dụng desktop đa nền tảng chạy trên Windows, macOS, Android và iOS từ một mã nguồn duy nhất. Bạn viết code một lần, chạy được nhiều nơi.
- **[Windows Presentation Foundation (WPF)](/dotnet/desktop/wpf/)** (Nền tảng trình bày Windows) -- xây dựng ứng dụng desktop giàu tính năng chỉ dành cho Windows, với **đồ họa tiên tiến** (có thể tùy chỉnh giao diện, animation, 3D) và **ràng buộc dữ liệu** (data binding -- tự động đồng bộ dữ liệu giữa giao diện và code).
- **[Windows Forms](/dotnet/desktop/winforms/)** (Biểu mẫu Windows) -- cung cấp cách thức đơn giản và trực quan nhất để tạo ứng dụng desktop trên Windows với **trình thiết kế giao diện kéo-thả** (drag-and-drop designer -- bạn kéo các nút, ô nhập liệu,... từ hộp công cụ vào form).

Bắt đầu: [Hướng dẫn .NET MAUI](/dotnet/maui/get-started/first-app).

## Ứng dụng di động

Xây dựng ứng dụng di động **gốc** (native -- được viết riêng cho một hệ điều hành, chạy nhanh và tận dụng được tối đa tính năng của thiết bị) cho iOS và Android bằng [.NET MAUI](/dotnet/maui/). .NET MAUI cho phép bạn chia sẻ mã nguồn giữa các nền tảng di động và desktop, đồng thời vẫn truy cập được các **API thiết bị gốc** (native device APIs -- các hàm lập trình có sẵn của hệ điều hành cho phép truy cập phần cứng) như camera, cảm biến (sensor), **GPS** (định vị toàn cầu) và nhiều hơn nữa.

Bắt đầu: [Xây dựng ứng dụng .NET MAUI đầu tiên của bạn](/dotnet/maui/get-started/first-app).

## Đám mây và microservices

**Cloud** (đám mây) -- các máy chủ từ xa qua Internet, cho phép bạn chạy ứng dụng mà không cần tự quản lý máy chủ vật lý. **Cloud-native** (ứng dụng gốc đám mây) là ứng dụng được thiết kế để chạy trên đám mây ngay từ đầu. **Microservices** (vi dịch vụ) -- kiến trúc chia ứng dụng lớn thành nhiều dịch vụ nhỏ độc lập, mỗi dịch vụ đảm nhiệm một chức năng riêng. C# rất phù hợp để xây dựng các ứng dụng gốc đám mây (cloud-native) và microservices:

- **[Azure SDK for .NET](../../azure/sdk/azure-sdk-for-dotnet.md)** (SDK = Software Development Kit) cung cấp các thư viện để làm việc với các **dịch vụ Azure** như **lưu trữ** (storage), **nhắn tin** (messaging) và **cơ sở dữ liệu** (database).
- **[Worker Services](../../core/extensions/workers.md)** cho phép bạn xây dựng các **dịch vụ nền** (background service) chạy lâu dài, có thể chạy trên đám mây hoặc **tại chỗ** (on-premises -- máy chủ đặt tại công ty bạn).
- **[Aspire](https://aspire.dev)** -- một bộ công cụ giúp đơn giản hóa việc xây dựng, chạy, triển khai (deploy -- đưa ứng dụng lên môi trường chạy thật) và gỡ lỗi (debug) các **ứng dụng phân tán** (distributed applications -- ứng dụng gồm nhiều dịch vụ chạy trên nhiều máy khác nhau).

Bắt đầu: [Bắt đầu với Azure và .NET](../../azure/index.yml).

## Trò chơi

C# là một trong những ngôn ngữ phổ biến nhất để **phát triển trò chơi** (game development):

- **[Unity](https://docs.unity3d.com/Manual/index.html)** - **Game engine** (công cụ tạo trò chơi -- phần mềm cung cấp các tính năng có sẵn như đồ họa, âm thanh, vật lý để bạn tập trung vào nội dung trò chơi) được sử dụng rộng rãi nhất cho trò chơi 2D và 3D, sử dụng C# làm **ngôn ngữ kịch bản** (scripting language -- viết code điều khiển hành vi trong trò chơi).
- **[MonoGame](https://docs.monogame.net/?page=main)** - Một **framework** (khung lập trình) mã nguồn mở để tạo trò chơi đa nền tảng, là phiên bản kế thừa của XNA.
- **[CryEngine](https://docs.cryengine.com/display/CEPROG/C%23+Programming)** - Game engine nổi tiếng với đồ họa cao cấp, hỗ trợ C# cho việc viết kịch bản trò chơi.

Bạn cũng có thể sử dụng [Visual Studio để phát triển trò chơi](https://visualstudio.microsoft.com/vs/features/game-development/?utm_medium=microsoft&utm_source=learn.microsoft.com&utm_campaign=inline+link) với các engine này.

## Internet of Things (IoT)

**IoT** (Internet of Things -- Internet vạn vật, mạng lưới các thiết bị vật lý được kết nối Internet như cảm biến, đèn thông minh, máy điều nhiệt,...). Điều khiển thiết bị và đọc dữ liệu cảm biến bằng cách sử dụng [thư viện IoT](../../iot/index.yml). Bạn có thể chạy ứng dụng C# trên các thiết bị như **Raspberry Pi** (một máy tính nhỏ gọn, giá rẻ, thường dùng cho các dự án IoT) và các **máy tính bảng đơn** (single-board computer -- máy tính chỉ có một bảng mạch duy nhất, như Raspberry Pi, Arduino) khác để xây dựng các giải pháp IoT.

Bắt đầu: [Hướng dẫn IoT](../../iot/tutorials/blink-led.md).

## Các bước tiếp theo

Giờ bạn đã biết mình có thể xây dựng những gì, hãy chọn bước tiếp theo phù hợp:

- **Học ngôn ngữ**: Bắt đầu với [hướng dẫn C# cho người mới bắt đầu](tutorials/index.md) để học các **kiến thức nền tảng** (fundamentals) về C# qua các bài tập tương tác.
- **Khám phá C#**: Đọc [Tổng quan về C#](overview.md) để có cái nhìn tổng quan về các tính năng chính của ngôn ngữ, từ cú pháp cơ bản đến pattern matching và async/await.
- **Đi sâu vào nền tảng**: Truy cập phần [Kiến thức nền tảng C#](../fundamentals/program-structure/index.md) để tìm hiểu sâu hơn về **hệ thống kiểu dữ liệu** (type system), **lập trình hướng đối tượng** (OOP), **xử lý lỗi** (error handling) và nhiều hơn nữa.
- **Đến từ ngôn ngữ khác?** Xem **lộ trình** (learning path) dành riêng cho lập trình viên [Java](tips-for-java-developers.md), [JavaScript/TypeScript](tips-for-javascript-developers.md) hoặc [Python](tips-for-python-developers.md) để thấy sự khác biệt và tận dụng kiến thức sẵn có.
