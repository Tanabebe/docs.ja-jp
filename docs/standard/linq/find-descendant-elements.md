---
title: 子孫要素を検索する方法 - LINQ to XML
description: この記事では、C# と Visual Basic で XPath と LINQ to XML クエリを使用し、指定の名前を持つ子孫要素をすべて検索する方法を紹介します。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b318da39-bb8b-4c56-a019-e13b12b01831
ms.openlocfilehash: 36547c4ad39953e25bf7a8d5f69aa4a712e51982
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "103412136"
---
# <a name="how-to-find-descendant-elements-linq-to-xml"></a><span data-ttu-id="8a2cd-103">子孫要素を検索する方法 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="8a2cd-103">How to find descendant elements (LINQ to XML)</span></span>

<span data-ttu-id="8a2cd-104">この記事では、C# と Visual Basic で XPath と LINQ to XML クエリを使用し、指定の名前を持つ子孫要素をすべて検索する方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="8a2cd-104">This article shows how to use XPath and LINQ to XML query, in C# and Visual Basic, to find all descendant elements that have a specified name.</span></span>

## <a name="example-find-descendant-elements-that-have-a-specified-name"></a><span data-ttu-id="8a2cd-105">例: 指定の名前を持つ子孫要素を検索する</span><span class="sxs-lookup"><span data-stu-id="8a2cd-105">Example Find descendant elements that have a specified name</span></span>

 <span data-ttu-id="8a2cd-106">この例では、LINQ to XML クエリと XPath を使用し、XML ドキュメント「[サンプル XML ファイル: 複数の購買発注書](sample-xml-file-multiple-purchase-orders.md)」で `Name` という名前を持つ子孫要素をすべて検索します。</span><span class="sxs-lookup"><span data-stu-id="8a2cd-106">This example shows how to use LINQ to XML query and XPath to find all descendant elements named `Name` in XML document [Sample XML file: Multiple purchase orders](sample-xml-file-multiple-purchase-orders.md).</span></span> <span data-ttu-id="8a2cd-107">XPath 式は `//Name` です。</span><span class="sxs-lookup"><span data-stu-id="8a2cd-107">The XPath expression is `//Name`.</span></span>

```csharp
XDocument po = XDocument.Load("PurchaseOrders.xml");

// LINQ to XML query
IEnumerable<XElement> list1 = po.Root.Descendants("Name");

// XPath expression
IEnumerable<XElement> list2 = po.XPathSelectElements("//Name");

if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list1)
    Console.WriteLine(el);
```

```vb
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")

' LINQ to XML query
Dim list1 As IEnumerable(Of XElement) = po...<Name>

' XPath expression
Dim list2 As IEnumerable(Of XElement) = po.XPathSelectElements("//Name")

If (list1.Count() = list2.Count() And _
        list1.Intersect(list2).Count() = list1.Count()) Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
For Each el As XElement In list1
    Console.WriteLine(el)
Next
```

<span data-ttu-id="8a2cd-108">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="8a2cd-108">This example produces the following output:</span></span>

```output
Results are identical
<Name>Ellen Adams</Name>
<Name>Tai Yee</Name>
<Name>Cristian Osorio</Name>
<Name>Cristian Osorio</Name>
<Name>Jessica Arnold</Name>
<Name>Jessica Arnold</Name>
```

## <a name="see-also"></a><span data-ttu-id="8a2cd-109">関連項目</span><span class="sxs-lookup"><span data-stu-id="8a2cd-109">See also</span></span>

- [<span data-ttu-id="8a2cd-110">XPath ユーザー向けの LINQ to XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8a2cd-110">LINQ to XML for XPath Users (Visual Basic)</span></span>](./comparison-xpath-linq-xml.md)
