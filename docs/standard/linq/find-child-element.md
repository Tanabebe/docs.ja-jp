---
title: 子要素を検索する方法 - LINQ to XML
description: この記事では、XPath の子要素軸と LINQ to XML の <xref:System.Xml.Linq.XContainer.Element%2A> メソッドを比較します。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4fa6182d-6196-4ed1-9c9e-82949ff89c71
ms.openlocfilehash: 34ddfd78489927a40128196a6fc80e822302428b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "103412148"
---
# <a name="how-to-find-a-child-element-linq-to-xml"></a><span data-ttu-id="88066-103">子要素を検索する方法 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="88066-103">How to find a child element (LINQ to XML)</span></span>

<span data-ttu-id="88066-104">この記事では、XPath の子要素軸と LINQ to XML の <xref:System.Xml.Linq.XContainer.Element%2A> メソッドを比較します。</span><span class="sxs-lookup"><span data-stu-id="88066-104">This article compares the XPath child element axis to the LINQ to XML <xref:System.Xml.Linq.XContainer.Element%2A> method.</span></span>

## <a name="example-find-a-child-element-in-an-xml-document"></a><span data-ttu-id="88066-105">例: XML ドキュメントで子要素を検索する</span><span class="sxs-lookup"><span data-stu-id="88066-105">Example: Find a child element in an XML document</span></span>

<span data-ttu-id="88066-106">この例では、XML ドキュメント「[サンプル XML ファイル: 複数の購買発注書](sample-xml-file-multiple-purchase-orders.md)」に含まれる子要素 `DeliveryNotes` を検索します。</span><span class="sxs-lookup"><span data-stu-id="88066-106">This example finds the child element `DeliveryNotes` in XML document [Sample XML file: Multiple purchase orders](sample-xml-file-multiple-purchase-orders.md).</span></span>

<span data-ttu-id="88066-107">XPath 式は `DeliveryNotes` です。</span><span class="sxs-lookup"><span data-stu-id="88066-107">The XPath expression is `DeliveryNotes`.</span></span>

```csharp
XDocument cpo = XDocument.Load("PurchaseOrders.xml");
XElement po = cpo.Root.Element("PurchaseOrder");

// LINQ to XML query
XElement el1 = po.Element("DeliveryNotes");

// XPath expression
XElement el2 = po.XPathSelectElement("DeliveryNotes");
// same as "child::DeliveryNotes"
// same as "./DeliveryNotes"

if (el1 == el2)
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
Console.WriteLine(el1);
```

```vb
Dim cpo As XDocument = XDocument.Load("PurchaseOrders.xml")
Dim po As XElement = cpo.Root.<PurchaseOrder>.FirstOrDefault

'LINQ to XML query
Dim el1 As XElement = po.<DeliveryNotes>.FirstOrDefault

' XPath expression
Dim el2 As XElement = po.XPathSelectElement("DeliveryNotes")
' same as "child::DeliveryNotes"
' same as "./DeliveryNotes"

If el1 Is el2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(el1)
```

<span data-ttu-id="88066-108">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="88066-108">This example produces the following output:</span></span>

```output
Results are identical
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>
```

## <a name="see-also"></a><span data-ttu-id="88066-109">関連項目</span><span class="sxs-lookup"><span data-stu-id="88066-109">See also</span></span>

- [<span data-ttu-id="88066-110">XPath ユーザー向けの LINQ to XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="88066-110">LINQ to XML for XPath Users (Visual Basic)</span></span>](./comparison-xpath-linq-xml.md)
