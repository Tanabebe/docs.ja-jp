---
title: XPath を使用して LINQ to XML にクエリを実行する方法 - LINQ to XML
description: XPath を使用して XML ツリーに対してクエリを実行できる拡張メソッドについて説明します。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: ee5af263-4ab1-45e5-b792-33a3221b426d
ms.openlocfilehash: 8189bcdd38f9242a5890837633bbec4e7f2fc601
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "103412083"
---
# <a name="how-to-query-linq-to-xml-using-xpath-linq-to-xml"></a><span data-ttu-id="486d6-103">XPath を使用して LINQ to XML にクエリを実行する方法 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="486d6-103">How to query LINQ to XML using XPath (LINQ to XML)</span></span>

<span data-ttu-id="486d6-104">この記事では、XPath を使用して XML ツリーに対してクエリを実行できる拡張メソッドについて説明します。</span><span class="sxs-lookup"><span data-stu-id="486d6-104">This article introduces the extension methods that enable you to query an XML tree by using XPath.</span></span> <span data-ttu-id="486d6-105">これらの拡張メソッドの使用に関する詳細については、<xref:System.Xml.XPath.Extensions?displayProperty=nameWithType> を参照してください。</span><span class="sxs-lookup"><span data-stu-id="486d6-105">For detailed information about using these extension methods, see <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.</span></span>

> [!NOTE]
> <span data-ttu-id="486d6-106">古いコードの広範な利用など、XPath を使用してクエリを実行する特別な理由がない限りは、XPath を LINQ to XML と共に使用することはお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="486d6-106">Unless you have a very specific reason for querying using XPath, such as extensive use of legacy code, using XPath with LINQ to XML isn't recommended.</span></span> <span data-ttu-id="486d6-107">XPath クエリは、LINQ to XML クエリよりもパフォーマンスが低くなります。</span><span class="sxs-lookup"><span data-stu-id="486d6-107">XPath queries won't perform as well as LINQ to XML queries.</span></span>

## <a name="example"></a><span data-ttu-id="486d6-108">例</span><span class="sxs-lookup"><span data-stu-id="486d6-108">Example</span></span>

<span data-ttu-id="486d6-109">次の例では、小さな XML ツリーを作成し、<xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> を使用して要素のセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="486d6-109">The following example creates a small XML tree and uses <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> to select a set of elements.</span></span>

```csharp
XElement root = new XElement("Root",
    new XElement("Child1", 1),
    new XElement("Child1", 2),
    new XElement("Child1", 3),
    new XElement("Child2", 4),
    new XElement("Child2", 5),
    new XElement("Child2", 6)
);
IEnumerable<XElement> list = root.XPathSelectElements("./Child2");
foreach (XElement el in list)
    Console.WriteLine(el);
```

```vb
Dim root As XElement = _
    <Root>
        <Child1>1</Child1>
        <Child1>2</Child1>
        <Child1>3</Child1>
        <Child2>4</Child2>
        <Child2>5</Child2>
        <Child2>6</Child2>
    </Root>

Dim list As IEnumerable(Of XElement) = root.XPathSelectElements("./Child2")
For Each el As XElement In list
    Console.WriteLine(el)
Next
```

<span data-ttu-id="486d6-110">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="486d6-110">This example produces the following output:</span></span>

```xml
<Child2>4</Child2>
<Child2>5</Child2>
<Child2>6</Child2>
```
