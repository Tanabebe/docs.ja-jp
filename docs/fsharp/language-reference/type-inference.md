---
title: 型推論
description: F# コンパイラが値、変数、パラメーター、戻り値の型を推定する方法について説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 4b18c1a67a8b7ddadb4fb334ea4736e9fd29feb0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630188"
---
# <a name="type-inference"></a>型推論

このトピックでは、F# コンパイラが値、変数、パラメーター、戻り値の型を推定する方法について説明します。

## <a name="type-inference-in-general"></a>型の推定一般

型の推定の概念は、コンパイラが最終的に型を推測できない場合を除いて、F# コンストラクトの型を指定する必要がないということです。 明示的な型情報を省略するのは、F# が動的型付け言語であるという意味でも、その F# の値の型付けが弱いという意味でもありません。 F# は、静的型付け言語です。つまり、コンパイラはコンパイル時に各コンストラクトに対して正確な型を推測します。 コンパイラが各コンストラクトの型を推測するのに十分な情報がない場合は、通常、コード内のどこかに明示的な型の注釈を追加することにより、追加の型情報を指定する必要があります。

## <a name="inference-of-parameter-and-return-types"></a>パラメーターと戻り値の型の推定

パラメーター リストでは、各パラメーターの型を指定する必要はありません。 それでも、F# は静的型付け言語であるため、すべての値と式にはコンパイル時に明確な型が指定されます。 明示的に指定しない型については、コンパイラがコンテキストに基づいて型を推定します。 型が指定されていない場合は、ジェネリックであると推定されます。 コード内で、ある値が一貫性のある方法で使用されていない場合 (ある値のすべての使用箇所で条件にかなう単一の推定型がない場合など)、コンパイラによりエラーが報告されます。

関数の戻り値の型は、関数に含まれている最後の式の型によって決まります。

たとえば、次のコードでは、リテラル `100` の型が `int` であるため、パラメーターの型 `a` と `b`、および戻り値の型はすべて `int` と推定されます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet301.fs)]

リテラルを変更することで、型の推定に影響を与えることができます。 サフィックス `u` を追加して `100` を `uint32` にする場合、`a`、`b`、戻り値の型は `uint32` と推定されます。

特定の型のみを処理する関数やメソッドなど、型に制限がある他の構造体を使用して、型の推定に影響を与えることもできます。

また、次の例に示すように、関数やメソッドのパラメーターまたは式の変数に明示的な型の注釈を適用することもできます。 異なる制約の間で競合が発生すると、エラーが発生します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet302.fs)]

また、すべてのパラメーターの後に型の注釈を指定して、関数の戻り値を明示的に指定することもできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet303.fs)]

パラメーターで型の注釈が役立つ一般的なケースは、パラメーターがオブジェクト型で、メンバーを使用する場合です。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet304.fs)]

## <a name="automatic-generalization"></a>自動ジェネリック化

関数コードがパラメーターの型に依存していない場合、コンパイラはパラメーターをジェネリックと見なします。 これは "*自動ジェネリック化*" と呼ばれ、複雑さを増大させることなくジェネリック コードを記述するための強力な機能となります。

たとえば、次の関数は、任意の型の 2 つのパラメーターを結合してタプルにします。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet305.fs)]

型は、次のように推定されます。

```fsharp
'a -> 'b -> 'a * 'b
```

## <a name="additional-information"></a>追加情報

型の推定については、F# 言語仕様でさらに詳しく説明されています。

## <a name="see-also"></a>関連項目

- [自動ジェネリック化](./generics/automatic-generalization.md)
