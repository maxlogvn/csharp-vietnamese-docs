---
title: Cú pháp được sử dụng bởi thuộc tính DebugView
description: Mô tả cú pháp đặc biệt được thuộc tính DebugView sử dụng để tạo ra biểu diễn dạng chuỗi của expression tree (cây biểu thức)
author: zspitz
ms.date: 03/06/2023
helpviewer_keywords:
- "expression trees"
- "debugview"
---
# Cú pháp DebugView

Thuộc tính **DebugView** (chỉ khả dụng khi đang gỡ lỗi) cung cấp bản kết xuất dạng chuỗi của expression tree (cây biểu thức). Hầu hết cú pháp khá dễ hiểu; các trường hợp đặc biệt được mô tả trong những phần sau.

Mỗi ví dụ đều có kèm một khối comment chứa nội dung của **DebugView**.

## ParameterExpression

Tên biến của [`ParameterExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.parameterexpression) được hiển thị với ký hiệu `$` ở đầu.

Nếu một parameter (tham số) không có tên, nó sẽ được gán một tên tự động sinh ra, chẳng hạn như `$var1` hoặc `$var2`.

```csharp
ParameterExpression numParam =  Expression.Parameter(typeof(int), "num");
/*
    $num
*/

ParameterExpression numParam =  Expression.Parameter(typeof(int));
/*
    $var1
*/
```

## ConstantExpression

Đối với các object (đối tượng) [`ConstantExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.constantexpression) đại diện cho giá trị số nguyên, chuỗi và `null`, giá trị của hằng số (constant) được hiển thị.

Đối với các kiểu số có hậu tố chuẩn như trong C# literals, hậu tố được thêm vào giá trị. Bảng dưới đây liệt kê các hậu tố tương ứng với các kiểu số khác nhau.

| Kiểu                                                 | Từ khoá                                                                            | Hậu tố |
|------------------------------------------------------|------------------------------------------------------------------------------------|--------|
| [`UInt32`](https://learn.microsoft.com/dotnet/api/system.uint32)    | [uint](../../language-reference/builtin-types/integral-numeric-types.md)           | U      |
| [`Int64`](https://learn.microsoft.com/dotnet/api/system.int64)     | [long](../../language-reference/builtin-types/integral-numeric-types.md)           | L      |
| [`UInt64`](https://learn.microsoft.com/dotnet/api/system.uint64)    | [ulong](../../language-reference/builtin-types/integral-numeric-types.md)          | UL     |
| [`Double`](https://learn.microsoft.com/dotnet/api/system.double)    | [double](../../language-reference/builtin-types/floating-point-numeric-types.md)   | D      |
| [`Single`](https://learn.microsoft.com/dotnet/api/system.single)    | [float](../../language-reference/builtin-types/floating-point-numeric-types.md)    | F      |
| [`Decimal`](https://learn.microsoft.com/dotnet/api/system.decimal)   | [decimal](../../language-reference/builtin-types/floating-point-numeric-types.md)  | M      |

```csharp
int num = 10;
ConstantExpression expr = Expression.Constant(num);
/*
    10
*/

double num = 10;
ConstantExpression expr = Expression.Constant(num);
/*
    10D
*/
```

## BlockExpression

Nếu kiểu của object (đối tượng) [`BlockExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.blockexpression) khác với kiểu của biểu thức cuối cùng trong khối (block), kiểu đó sẽ được hiển thị trong dấu ngoặc nhọn (`<` và `>`). Nếu không, kiểu của object [`BlockExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.blockexpression) sẽ không được hiển thị.

```csharp
BlockExpression block = Expression.Block(Expression.Constant("test"));
/*
    .Block() {
        "test"
    }
*/

BlockExpression block =  Expression.Block(typeof(Object), Expression.Constant("test"));
/*
    .Block<System.Object>() {
        "test"
    }
*/
```

## LambdaExpression

Các object (đối tượng) [`LambdaExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression) được hiển thị cùng với kiểu delegate (uỷ quyền) của chúng.

Nếu một biểu thức lambda (lambda expression) không có tên, nó sẽ được gán một tên tự động sinh ra, chẳng hạn như `#Lambda1` hoặc `#Lambda2`.

```csharp
LambdaExpression lambda =  Expression.Lambda<Func<int>>(Expression.Constant(1));
/*
    .Lambda #Lambda1<System.Func'1[System.Int32]>() {
        1
    }
*/

LambdaExpression lambda =  Expression.Lambda<Func<int>>(Expression.Constant(1), "SampleLambda", null);
/*
    .Lambda #SampleLambda<System.Func'1[System.Int32]>() {
        1
    }
*/
```

## LabelExpression

Nếu bạn chỉ định một giá trị mặc định cho object (đối tượng) [`LabelExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.labelexpression), giá trị này sẽ được hiển thị trước object [`LabelTarget`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.labeltarget).

Token `.Label` đánh dấu điểm bắt đầu của nhãn (label). Token `.LabelTarget` đánh dấu đích đến để nhảy tới.

Nếu một nhãn không có tên, nó sẽ được gán một tên tự động sinh ra, chẳng hạn như `#Label1` hoặc `#Label2`.

```csharp
LabelTarget target = Expression.Label(typeof(int), "SampleLabel");
BlockExpression block = Expression.Block(
    Expression.Goto(target, Expression.Constant(0)),
    Expression.Label(target, Expression.Constant(-1))
);
/*
    .Block() {
        .Goto SampleLabel { 0 };
        .Label
            -1
        .LabelTarget SampleLabel:
    }
*/

LabelTarget target = Expression.Label();
BlockExpression block = Expression.Block(
    Expression.Goto(target),
    Expression.Label(target)
);
/*
    .Block() {
        .Goto #Label1 { };
        .Label
        .LabelTarget #Label1:
    }
*/
```

## Checked Operators

Các toán tử checked (kiểm tra tràn số) được hiển thị với ký hiệu `#` ở phía trước toán tử. Ví dụ, toán tử cộng checked được hiển thị là `#+`.

```csharp
Expression expr = Expression.AddChecked( Expression.Constant(1), Expression.Constant(2));
/*
    1 #+ 2
*/

Expression expr = Expression.ConvertChecked( Expression.Constant(10.0), typeof(int));
/*
    #(System.Int32)10D
*/
```
