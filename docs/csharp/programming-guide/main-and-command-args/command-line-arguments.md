---
title: コマンド ライン引数 - C# プログラミング ガイド
description: コマンド ライン引数について説明します。 コンソール アプリケーションでコマンド ライン引数を使用する例をご覧ください。
ms.date: 03/11/2021
helpviewer_keywords:
- command-line arguments [C#]
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
ms.openlocfilehash: f495efb3bc2c76a98f74c173d5b777ebe383edcb
ms.sourcegitcommit: e3cf8227573e13b8e1f4e3dc007404881cdafe47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2021
ms.locfileid: "103190412"
---
# <a name="command-line-arguments-c-programming-guide"></a>コマンド ライン引数 (C# プログラミング ガイド)

`Main` メソッドに引数を渡すには、次のいずれかの方法でメソッドを定義します。

| `Main` メソッド コード                 | `Main` シグネチャ                             |
|------------------------------------|----------------------------------------------|
| 戻り値がなく、`await` を使用しない | `static void Main(string[] args)`            |
| 戻り値があり、`await` を使用しない    | `static int Main(string[] args)`             |
| 戻り値がなく、`await` を使用する      | `static async Task Main(string[] args)`      |
| 戻り値があり、`await` を使用する         | `static async Task<int> Main(string[] args)` |

引数が使用されない場合、メソッド シグネチャから `args` を省略し、少しばかり簡単なコードにすることができます。

| `Main` メソッド コード                 | `Main` シグネチャ                |
|------------------------------------|---------------------------------|
| 戻り値がなく、`await` を使用しない | `static void Main()`            |
| 戻り値があり、`await` を使用しない    | `static int Main()`             |
| 戻り値がなく、`await` を使用する      | `static async Task Main()`      |
| 戻り値があり、`await` を使用する         | `static async Task<int> Main()` |

> [!NOTE]
> Windows フォーム アプリケーションの `Main` メソッドでコマンド ライン引数を有効にするには、*program.cs* の `Main` のシグネチャを手動で変更する必要があります。 Windows フォーム デザイナーが生成するコードは、入力パラメーターなしの `Main` を作成します。 <xref:System.Environment.CommandLine%2A?displayProperty=nameWithType> または <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=nameWithType> を使用して、コンソールまたは Windows アプリケーション内の任意の場所からコマンド ライン引数にアクセスすることもできます。

`Main` メソッドのパラメーターは <xref:System.String> の配列で、コマンド ライン引数を表しています。 通常は、`Length` プロパティを調べて引数があるかどうかを確認します。次はその例です。

[!code-csharp[csProgGuideMain#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#4)]

> [!TIP]
> `args` 配列を null にすることはできません。 そのため、null チェックを行わずに `Length` プロパティに安全にアクセスできます。

また、<xref:System.Convert> クラスまたは `Parse` メソッドを使って、文字列型の引数を数値型に変換できます。 たとえば、次のステートメントでは、`string` メソッドを使用して `long` を <xref:System.Int64.Parse%2A> 値に変換します。

```csharp
long num = Int64.Parse(args[0]);
```

C# の `long` 型を使うこともできます。これは `Int64` のエイリアスです。

```csharp
long num = long.Parse(args[0]);
```

また、同じ変換に `Convert` クラスの `ToInt64` メソッドを使うこともできます。

```csharp
long num = Convert.ToInt64(s);
```

詳細については、次のトピックを参照してください。 <xref:System.Int64.Parse%2A> および <xref:System.Convert>

## <a name="example"></a>例

コンソール アプリケーションでコマンド ライン引数を使用する方法の例を次に示します。 アプリケーションは、実行時に引数を 1 つ受け取り、整数に変換し、その値の階乗を計算しています。 引数がない場合は、アプリケーションの正しい使用方法を説明するメッセージを表示します。

コマンド プロンプトからアプリケーションをコンパイルして実行するには、次の手順を実行します。

1. 次のコードをテキスト エディターに貼り付け、*Factorial.cs* という名前でテキスト ファイルとして保存します。

     [!code-csharp[csProgGuideMain#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class1.cs#16)]

2. **[スタート]** 画面または **[スタート]** メニューから、Visual Studio の **[開発者コマンド プロンプト]** ウィンドウを開き、先ほど作成したファイルが含まれているフォルダーに移動します。

3. 次のコマンドを入力してアプリケーションをコンパイルします。
  
     `csc Factorial.cs`  
  
     アプリケーションにコンパイル エラーがなければ、*Factorial.exe* という名前の実行可能ファイルが作成されます。
  
4. 3 の階乗を計算する次のコマンドを入力します。
  
     `Factorial 3`  
  
5. 次の出力が生成されます: `The factorial of 3 is 6.`

> [!NOTE]
> Visual Studio でアプリケーションを実行する場合、「[[デバッグ] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/debug-page-project-designer)」のコマンド ライン引数を指定できます。

## <a name="see-also"></a>関連項目

- <xref:System.Environment?displayProperty=nameWithType>
- [C# プログラミング ガイド](../index.md)
- [Main() とコマンドライン引数](index.md)
- [コマンド ライン引数を表示する方法](how-to-display-command-line-arguments.md)
- [Main() の戻り値](main-return-values.md)
- [クラス](../classes-and-structs/classes.md)
