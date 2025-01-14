---
title: 文字列を型に変換する
description: .NET での文字列の解析について理解します。 解析では、.NET の基本データ型を表す文字列をその基本データ型に変換します。 解析は書式設定の逆の操作です。
ms.date: 03/30/2017
ms.topic: conceptual
helpviewer_keywords:
- parsing strings, about parsing strings
- IFormatProvider interface, parsing strings
- base types, parsing strings
- Parse method
- parsing strings
ms.assetid: 5e758b41-db93-456b-8999-99b7304b090d
ms.openlocfilehash: ff357f8b8225c84e2f6c0e022b269f0ab774dfed
ms.sourcegitcommit: 4313614f57690f9a5119a37314f0a1fd738ebda2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98692852"
---
# <a name="parse-strings-in-net"></a>.NET で文字列を解析する

"*解析*" 操作により、.NET の基本データ型を表す文字列が、その基本データ型に変換されます。 たとえば、文字列を浮動小数点数や日付と時刻の値に変換するには、解析操作を使用します。 解析操作を実行するには、`Parse` メソッドがよく使用されます。 解析は書式設定の逆の操作 (基本データ型のその文字列形式への変換を含む) であるため、多くの同じ規則が適用されます。 カルチャに依存する書式情報を指定するために、書式設定で <xref:System.IFormatProvider> インターフェイスを実装するオブジェクトを使用するのと同じように、解析でも <xref:System.IFormatProvider> インターフェイスを実装するオブジェクトを使用し、文字列形式を解釈する方法を決定します。 詳細については、[型の書式設定](formatting-types.md)に関するページをご覧ください。

## <a name="in-this-section"></a>このセクションの内容

 [数値文字列の解析](parsing-numeric.md)\
 文字列を .NET 数値型に変換する方法について説明します。

 [日付と時刻文字列の解析](parsing-datetime.md)\
 文字列を .NET **DateTime** 型に変換する方法について説明します。

 [その他の文字列の解析](parsing-other.md)\
 文字列を **Char** 型、**Boolean** 型、**Enum** 型に変換する方法について説明します。

## <a name="related-sections"></a>関連項目

 [型の書式設定](formatting-types.md)\
 書式指定子や書式プロバイダーなどの基本書式の概念について説明します。

 [.NET での型変換](type-conversion.md)\
 型に変換する方法について説明します。
