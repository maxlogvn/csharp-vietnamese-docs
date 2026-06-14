---
title: Cấu trúc dữ liệu của expression tree
description: Tìm hiểu về expression tree và cách chúng hữu ích trong việc chuyển đổi thuật toán để thực thi ở môi trường bên ngoài cũng như kiểm tra mã trước khi thực thi.
ms.date: 03/06/2023
---
# Expression tree (cây biểu thức) - dữ liệu định nghĩa mã

**Expression Tree (cây biểu thức)** là một cấu trúc dữ liệu định nghĩa mã. Expression tree dựa trên cùng những cấu trúc mà trình biên dịch sử dụng để phân tích mã và tạo ra đầu ra đã biên dịch. Khi đọc bài viết này, bạn sẽ thấy khá nhiều điểm tương đồng giữa expression tree và các kiểu được dùng trong Roslyn API để xây dựng [Analyzers và CodeFixes](https://github.com/dotnet/roslyn-analyzers). (Analyzers và CodeFixes là những gói NuGet thực hiện phân tích tĩnh trên mã nguồn và đề xuất các bản sửa lỗi tiềm năng cho lập trình viên.) Ý tưởng là tương tự, và kết quả cuối cùng là một cấu trúc dữ liệu cho phép kiểm tra mã nguồn một cách có ý nghĩa. Tuy nhiên, expression tree dựa trên một bộ class (lớp) và API khác với Roslyn API. Dưới đây là một dòng mã:

```csharp
var sum = 1 + 2;
```

Nếu bạn phân tích dòng mã trên dưới dạng một expression tree, cây này sẽ chứa nhiều node (nút). Nút ngoài cùng là một câu lệnh khai báo biến có gán giá trị (`var sum = 1 + 2;`). Nút ngoài cùng này chứa một số nút con: một khai báo biến, một toán tử gán, và một biểu thức đại diện cho vế phải của dấu bằng. Biểu thức đó lại được chia nhỏ thành các biểu thức con đại diện cho phép cộng, toán hạng trái và toán hạng phải của phép cộng.

Hãy tìm hiểu sâu hơn một chút về các biểu thức tạo nên vế phải của dấu bằng. Biểu thức là `1 + 2`, một binary expression (biểu thức nhị phân). Cụ thể hơn, nó là một binary addition expression (biểu thức cộng nhị phân). Một biểu thức cộng nhị phân có hai nút con, đại diện cho nút trái và nút phải của phép cộng. Ở đây, cả hai nút đều là constant expression (biểu thức hằng): toán hạng trái là giá trị `1`, và toán hạng phải là giá trị `2`.

Nhìn trực quan, toàn bộ câu lệnh là một cây: bạn có thể bắt đầu từ nút gốc, và di chuyển đến từng nút trong cây để thấy mã tạo nên câu lệnh:

- Câu lệnh khai báo biến có gán giá trị (`var sum = 1 + 2;`)
  - Khai báo kiểu biến ngầm định (`var sum`)
    - Từ khoá var ngầm định (`var`)
    - Khai báo tên biến (`sum`)
  - Toán tử gán (`=`)
  - Biểu thức cộng nhị phân (`1 + 2`)
    - Toán hạng trái (`1`)
    - Toán tử cộng (`+`)
    - Toán hạng phải (`2`)

Cây trên có vẻ phức tạp, nhưng nó rất mạnh mẽ. Theo cùng cách này, bạn có thể phân rã những biểu thức phức tạp hơn nhiều. Hãy xem xét biểu thức sau:

```csharp
var finalAnswer = this.SecretSauceFunction(
    currentState.createInterimResult(), currentState.createSecondValue(1, 2),
    decisionServer.considerFinalOptions("hello")) +
    MoreSecretSauce('A', DateTime.Now, true);
```

Biểu thức trên cũng là một khai báo biến có gán giá trị. Trong trường hợp này, vế phải của phép gán là một cây phức tạp hơn nhiều. Chúng ta sẽ không phân rã biểu thức này, nhưng hãy thử hình dung các nút khác nhau có thể là gì. Có những lời gọi method (phương thức) sử dụng đối tượng hiện tại làm receiver (bộ tiếp nhận), một cái có receiver `this` tường minh, một cái không có. Có những lời gọi method sử dụng các đối tượng receiver khác, có các tham số hằng thuộc nhiều kiểu khác nhau. Và cuối cùng, có một toán tử cộng nhị phân. Tuỳ thuộc vào kiểu trả về của `SecretSauceFunction()` hoặc `MoreSecretSauce()`, toán tử cộng nhị phân đó có thể là một lời gọi method tới một toán tử cộng bị ghi đè (overridden), dẫn đến một lời gọi method tĩnh tới toán tử cộng nhị phân được định nghĩa cho một class.

Dù có vẻ phức tạp như vậy, biểu thức trên vẫn tạo ra một cấu trúc cây có thể duyệt dễ dàng như ví dụ đầu tiên. Bạn cứ tiếp tục duyệt qua các nút con để tìm các nút lá trong biểu thức. Các nút cha có tham chiếu đến nút con của chúng, và mỗi nút có một thuộc tính mô tả nó là loại nút gì.

Cấu trúc của một expression tree rất nhất quán. Một khi bạn đã nắm được những điều cơ bản, bạn sẽ hiểu được ngay cả những mã phức tạp nhất khi nó được biểu diễn dưới dạng expression tree. Sự thanh lịch trong cấu trúc dữ liệu này giải thích cách trình biên dịch C# phân tích những chương trình C# phức tạp nhất và tạo ra đầu ra chính xác từ mã nguồn phức tạp đó.

Một khi bạn đã quen với cấu trúc của expression tree, bạn sẽ thấy rằng kiến thức bạn có được sẽ nhanh chóng giúp bạn làm việc với nhiều tình huống nâng cao hơn. Expression tree có sức mạnh đáng kinh ngạc.

Ngoài việc chuyển đổi thuật toán để thực thi trong các môi trường khác, expression tree còn giúp việc viết các thuật toán kiểm tra mã trước khi thực thi trở nên dễ dàng hơn. Bạn viết một method nhận các biểu thức làm tham số và sau đó kiểm tra các biểu thức đó trước khi thực thi mã. Expression Tree là một biểu diễn đầy đủ của mã: bạn thấy giá trị của bất kỳ biểu thức con nào. Bạn thấy tên của method và thuộc tính. Bạn thấy giá trị của bất kỳ biểu thức hằng nào. Bạn có thể chuyển đổi một expression tree thành một delegate (uỷ quyền) có thể thực thi, và chạy mã đó.

API dành cho Expression Tree cho phép bạn tạo ra các cây biểu diễn hầu hết mọi cấu trúc mã hợp lệ. Tuy nhiên, để giữ mọi thứ đơn giản nhất có thể, một số thành ngữ C# không thể được tạo trong expression tree. Một ví dụ là asynchronous expression (biểu thức bất đồng bộ) (sử dụng từ khoá `async` và `await`). Nếu nhu cầu của bạn yêu cầu các thuật toán bất đồng bộ, bạn sẽ cần thao tác trực tiếp với các đối tượng `Task`, thay vì dựa vào hỗ trợ của trình biên dịch. Một ví dụ khác là tạo vòng lặp. Thông thường, bạn tạo các vòng lặp bằng cách sử dụng `for`, `foreach`, `while` hoặc `do`. Như bạn sẽ thấy [sau trong loạt bài này](expression-trees-building.md), API cho expression tree hỗ trợ một biểu thức vòng lặp duy nhất, với các biểu thức `break` và `continue` để điều khiển việc lặp lại vòng lặp.

Một điều bạn không thể làm là sửa đổi một expression tree. Expression Tree là những cấu trúc dữ liệu bất biến (immutable). Nếu bạn muốn thay đổi (mutate) một expression tree, bạn phải tạo một cây mới là bản sao của cây gốc, nhưng với những thay đổi bạn mong muốn.
