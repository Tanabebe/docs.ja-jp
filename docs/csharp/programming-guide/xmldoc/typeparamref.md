---
title: <typeparamref> - C# プログラミング ガイド
description: XML <typeparamref> タグについて説明します。 このタグを使用すると、ドキュメント ファイルを使用するときに、何らかの方法で単語の書式を指定できます (斜体など)。
ms.date: 07/20/2015
f1_keywords:
- typeparamref
helpviewer_keywords:
- typeparamref C# XML tag
- <typeparamref> C# XML tag
ms.assetid: 6d8ffc58-12c5-4688-8db6-833a7ded5886
ms.openlocfilehash: 1bb9a73f4122f3b9d521565a7172a9b8f75f7a98
ms.sourcegitcommit: 0bb8074d524e0dcf165430b744bb143461f17026
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2021
ms.locfileid: "103477668"
---
# <a name="typeparamref-c-programming-guide"></a>\<typeparamref> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<typeparamref name="name"/>
```

## <a name="parameters"></a>パラメーター

- `name`

  型パラメーターの名前。 名前は二重引用符 (" ") で囲みます。

## <a name="remarks"></a>Remarks

ジェネリック型およびメソッドの型パラメーターの詳細については、「[ジェネリック (C# プログラミング ガイド)](../generics/index.md)」を参照してください。

ドキュメント ファイルを使用するときに何らかの方法で単語の書式 (斜体など) を指定するには、このタグを使用します。

コンパイル時に [**DocumentationFile**](../../language-reference/compiler-options/output.md#documentationfile) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

[!code-csharp[csProgGuideDocComments#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#13)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
