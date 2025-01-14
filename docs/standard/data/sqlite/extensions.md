---
title: 拡張機能
ms.date: 12/08/2020
description: SQLite 拡張機能を読み込む方法について説明します。
ms.openlocfilehash: 45ef5d2e5e8ea1f25866d3239e06fc87d8a91d44
ms.sourcegitcommit: e3cf8227573e13b8e1f4e3dc007404881cdafe47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2021
ms.locfileid: "103190048"
---
# <a name="extensions"></a>拡張機能

SQLite では、実行時の拡張機能の読み込みがサポートされています。 拡張機能には、追加の SQL 関数、照合順序、仮想テーブルなどが含まれます。

.NET Core には、参照されている NuGet パッケージなどの追加の場所でネイティブ ライブラリを見つけるための、追加のロジックがあります。 ただし、SQLite ではこのロジックを利用できません。プラットフォーム API を直接呼び出して、ライブラリが読み込まれます。 このため、SQLite 拡張機能を読み込む前に、PATH、LD_LIBRARY_PATH、または DYLD_LIBRARY_PATH の各環境変数の変更が必要になる場合があります。 GitHub には、参照されている NuGet パッケージ内の現在のランタイムのバイナリの検索方法を示す[サンプル](https://github.com/dotnet/docs/blob/main/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs)があります。

拡張機能を読み込むには、<xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> メソッドを呼び出します。 Microsoft.Data.Sqlite を使用すると、接続をいったん閉じて再び開いた場合でも、拡張機能は読み込まれたままになります。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs?name=snippet_LoadExtension)]

> [!NOTE]
> LoadExtension メソッドはバージョン 3.0 で追加されました。

## <a name="see-also"></a>関連項目

* [実行時に読み込み可能な拡張機能](https://www.sqlite.org/loadext.html)
