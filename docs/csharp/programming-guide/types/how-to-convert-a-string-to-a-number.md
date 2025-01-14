---
title: 文字列を数値に変換する方法 - C# プログラミング ガイド
description: C# で Parse、TryParse、または Convert クラスのメソッドを呼び出すことによって、文字列を数値に変換する方法について説明します。
ms.date: 02/16/2021
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.topic: how-to
ms.custom: contperf-fy21q3
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
ms.openlocfilehash: 0fffd080f502646b6541ad7b2236359e9d85b884
ms.sourcegitcommit: 42d436ebc2a7ee02fc1848c7742bc7d80e13fc2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "102103219"
---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>文字列を数値に変換する方法 (C# プログラミング ガイド)

`string` を数値に変換するには、数値型 (`int`、`long`、`double` など) で見つかる `Parse` または `TryParse` メソッドを呼び出すか、<xref:System.Convert?displayProperty=nameWithType> クラスのメソッドを使用します。
  
`TryParse` メソッド (たとえば [`int.TryParse("11", out number)`](xref:System.Int32.TryParse%2A)) または `Parse` メソッド (たとえば [`var number = int.Parse("11")`](xref:System.Int32.Parse%2A)) を呼び出す方がいくらか効率的で簡単です。 <xref:System.IConvertible> を実装している一般的なオブジェクトでは、<xref:System.Convert> メソッドを使用するのがより便利です。
  
文字列に含まれていると思われる数値型 (<xref:System.Int32?displayProperty=nameWithType> 型など) の `Parse` または `TryParse` メソッドを使用します。  <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> メソッドは、<xref:System.Int32.Parse%2A> を内部的に使用します。  `Parse` メソッドからは、変換された数値が返されます。`TryParse` メソッドからは変換が成功したかどうかを示すブール値が返され、変換された数値は `out` パラメーターで戻されます。 文字列の形式が無効である場合、`Parse` では例外がスローされますが、`TryParse` では `false` が返されます。 `Parse` メソッドを呼び出すときは常に例外処理を使用し、解析操作が失敗したときの <xref:System.FormatException> をキャッチする必要があります。
  
## <a name="call-parse-or-tryparse-methods"></a>Parse または TryParse メソッドを呼び出す

文字列の先頭と末尾の空白文字は、`Parse` および `TryParse` メソッドによって無視されますが、その他のすべての文字は、適切な数値型 (`int`、`long`、`ulong`、`float`、`decimal` など) を形成する文字である必要があります。  数値を形成する文字列内に空白文字があると、エラーになります。  たとえば、"10"、"10.3"、または "  10  " を解析するために `decimal.TryParse` を使用することはできますが、"10X"、"1 0" (埋め込みスペースに注意)、"10 .3" (埋め込みスペースに注意)、"10e1" (この場合は `float.TryParse` を使用) などからこのメソッドを使用して 10 を解析することはできません。 値が `null` または <xref:System.String.Empty?displayProperty=nameWithType> の文字列は正常に解析できません。 <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> メソッドを呼び出すことで、解析を試みる前に null または空の文字列を確認できます。

次の例は、`Parse` および `TryParse` の呼び出しの成功例と失敗例の両方を示しています。

[!code-csharp[Parse and TryParse](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse/program.cs)]

次の例は、先頭に数字 (16 進数文字を含む)、末尾に数字以外の文字を含むと予想される文字列を解析する 1 つのアプローチを示しています。 <xref:System.Int32.TryParse%2A> メソッドを呼び出す前に、文字列の先頭から新しい文字列に有効な文字を割り当てます。 解析対象の文字列には少数の文字が含まれるので、例では <xref:System.String.Concat%2A?displayProperty=nameWithType> メソッドを呼び出して新しい文字列に有効な文字を割り当てます。 より大きな文字列の場合は、代わりに <xref:System.Text.StringBuilder> クラスを使用できます。

[!code-csharp[Removing invalid characters](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse2/program.cs)]

## <a name="call-convert-methods"></a>Convert メソッドを呼び出す

文字列を数値に変換するために使用できる <xref:System.Convert> クラスのメソッドの一部を次の表に示します。

| 数値型 | メソッド                                             |
|--------------|----------------------------------------------------|
| `decimal`    | <xref:System.Convert.ToDecimal%28System.String%29> |
| `float`      | <xref:System.Convert.ToSingle%28System.String%29>  |
| `double`     | <xref:System.Convert.ToDouble%28System.String%29>  |
| `short`      | <xref:System.Convert.ToInt16%28System.String%29>   |
| `int`        | <xref:System.Convert.ToInt32%28System.String%29>   |
| `long`       | <xref:System.Convert.ToInt64%28System.String%29>   |
| `ushort`     | <xref:System.Convert.ToUInt16%28System.String%29>  |
| `uint`       | <xref:System.Convert.ToUInt32%28System.String%29>  |
| `ulong`      | <xref:System.Convert.ToUInt64%28System.String%29>  |

次の例では、<xref:System.Convert.ToInt32%28System.String%29?displayProperty=nameWithType> メソッドを呼び出して、入力文字列を [int](../../language-reference/builtin-types/integral-numeric-types.md) に変換します。例では、このメソッドからスローされる可能性のある最も一般的な 2 種類の例外 (<xref:System.FormatException> と <xref:System.OverflowException>) をキャッチします。 <xref:System.Int32.MaxValue?displayProperty=nameWithType> を超えずに結果の数値を増やすことができる場合、例では結果に 1 を加算し、出力を表示します。

[!code-csharp[Parsing with Convert methods](~/samples/snippets/csharp/programming-guide/string-to-number/convert/program.cs)]
