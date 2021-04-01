---
title: 特定の要素名を持つ子孫を検索する方法 - LINQ to XML
description: 特定の名前を持つ子孫をすべて見つけるには、すべての子孫を対象に同じ処理を繰り返すより、XContainer.Descendants を使用した方が簡単です。
ms.date: 07/20/2015
ms.assetid: f684da20-bee9-47f5-9607-7e3fd7e67470
ms.openlocfilehash: 68d5ed3379e11872458ce98421e62e3cd53c1ab5
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "103365986"
---
# <a name="how-to-find-descendants-with-a-specific-element-name-linq-to-xml"></a><span data-ttu-id="83126-103">特定の要素名を持つ子孫を検索する方法 - (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="83126-103">How to find descendants with a specific element name (LINQ to XML)</span></span>

<span data-ttu-id="83126-104">特定の名前を持つ子孫をすべて見つけなければならない場合があります。</span><span class="sxs-lookup"><span data-stu-id="83126-104">Sometimes you want to find all descendants with a specific name.</span></span> <span data-ttu-id="83126-105">すべての子孫を反復処理するコードを記述することもできますが、<xref:System.Xml.Linq.XContainer.Descendants%2A> 軸を使用する方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="83126-105">You could write code to iterate through all of the descendants, but it's easier to use the <xref:System.Xml.Linq.XContainer.Descendants%2A> axis.</span></span>

## <a name="example-find-descendants-with-a-specific-element-name"></a><span data-ttu-id="83126-106">例: 特定の要素名を持つ子孫を見つける</span><span class="sxs-lookup"><span data-stu-id="83126-106">Example: Find descendants with a specific element name</span></span>

<span data-ttu-id="83126-107">特定の要素名を持つ子孫を見つける方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="83126-107">The following example shows how to find descendants with a specific element name.</span></span>

```csharp
XElement root = XElement.Parse(@"<root>
  <para>
    <r>
      <t>Some text </t>
    </r>
    <n>
      <r>
        <t>that's broken up into </t>
      </r>
    </n>
    <n>
      <r>
        <t>multiple segments.</t>
      </r>
    </n>
  </para>
</root>");
IEnumerable<string> textSegs =
    from seg in root.Descendants("t")
    select (string)seg;

string str = textSegs.Aggregate(new StringBuilder(),
    (sb, i) => sb.Append(i),
    sp => sp.ToString()
);

Console.WriteLine(str);
```

```vb
Dim root As XElement = _
    <root>
        <para>
            <r>
                <t>Some text </t>
            </r>
            <n>
                <r>
                    <t>that's broken up into </t>
                </r>
            </n>
            <n>
                <r>
                    <t>multiple segments.</t>
                </r>
            </n>
        </para>
    </root>

Dim textSegs As IEnumerable(Of String) = _
    From seg In root...<t> _
    Select seg.Value

Dim str As String = textSegs.Aggregate( _
    New StringBuilder, _
    Function(sb, i) sb.Append(i), _
    Function(sb) sb.ToString)

Console.WriteLine(str)
```

<span data-ttu-id="83126-108">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="83126-108">This example produces the following output:</span></span>

```output
Some text that's broken up into multiple segments.

## Example: Find when the XML is in a namespace

The following example shows the same query for XML that's in a namespace. For more information, see [Namespaces overview](namespaces-overview.md).

```csharp
XElement root = XElement.Parse(@"<root xmlns='http://www.adatum.com'>
  <para>
    <r>
      <t>Some text </t>
    </r>
    <n>
      <r>
        <t>that's broken up into </t>
      </r>
    </n>
    <n>
      <r>
        <t>multiple segments.</t>
      </r>
    </n>
  </para>
</root>");
XNamespace ad = "http://www.adatum.com";
IEnumerable<string> textSegs =
    from seg in root.Descendants(ad + "t")
    select (string)seg;

string str = textSegs.Aggregate(new StringBuilder(),
    (sb, i) => sb.Append(i),
    sp => sp.ToString()
);

Console.WriteLine(str);
```

```vb
Imports <xmlns='http://www.adatum.com'>

Module Module1
    Sub Main()
        Dim root As XElement = _
            <root>
                <para>
                    <r>
                        <t>Some text </t>
                    </r>
                    <n>
                        <r>
                            <t>that's broken up into </t>
                        </r>
                    </n>
                    <n>
                        <r>
                            <t>multiple segments.</t>
                        </r>
                    </n>
                </para>
            </root>

        Dim textSegs As IEnumerable(Of String) = _
            From seg In root...<t> _
            Select seg.Value

        Dim str As String = textSegs.Aggregate( _
            New StringBuilder, _
            Function(sb, i) sb.Append(i), _
            Function(sb) sb.ToString)

        Console.WriteLine(str)
    End Sub
End Module
```

<span data-ttu-id="83126-109">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="83126-109">This example produces the following output:</span></span>

```output
Some text that's broken up into multiple segments.
```

## <a name="see-also"></a><span data-ttu-id="83126-110">関連項目</span><span class="sxs-lookup"><span data-stu-id="83126-110">See also</span></span>

- <xref:System.Xml.Linq.XContainer.Descendants%2A>
