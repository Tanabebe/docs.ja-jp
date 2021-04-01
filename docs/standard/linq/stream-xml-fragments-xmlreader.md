---
title: XmlReader から XML フラグメントをストリーム配信する方法 - LINQ to XML
description: C# および Visual Basic でカスタムの軸メソッドを使用し、XmlReader から XML フラグメントをストリーム配信できます。 これは、XML ツリー全体をメモリに読み込めるときに機能する手法です。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
ms.openlocfilehash: e3a7a6260c66f0295216552c6aa56f71a8536bdf
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "103411978"
---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-linq-to-xml"></a><span data-ttu-id="77d6a-104">XmlReader から XML フラグメントをストリーム配信する方法 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="77d6a-104">How to stream XML fragments from an XmlReader (LINQ to XML)</span></span>

<span data-ttu-id="77d6a-105">大きな XML ファイルを処理する必要があるときに、XML ツリー全体をメモリに読み込むことができない場合があります。</span><span class="sxs-lookup"><span data-stu-id="77d6a-105">When you have to process large XML files, it might not be feasible to load the whole XML tree into memory.</span></span> <span data-ttu-id="77d6a-106">この記事では、C# および Visual Basic で <xref:System.Xml.XmlReader> を使用してフラグメントをストリーム配信する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-106">This article shows how to stream fragments using an <xref:System.Xml.XmlReader> in C# and Visual Basic.</span></span>

<span data-ttu-id="77d6a-107"><xref:System.Xml.XmlReader> を使用して <xref:System.Xml.Linq.XElement> オブジェクトを読み取るための最も効果的な方法の 1 つは、カスタムの軸メソッドを独自に記述することです。</span><span class="sxs-lookup"><span data-stu-id="77d6a-107">One of the most effective ways to use an <xref:System.Xml.XmlReader> to read <xref:System.Xml.Linq.XElement> objects is to write your own custom axis method.</span></span> <span data-ttu-id="77d6a-108">一般に軸メソッドは、この記事の例で示すように、<xref:System.Xml.Linq.XElement> の <xref:System.Collections.Generic.IEnumerable%601> などのコレクションを返します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-108">An axis method typically returns a collection such as <xref:System.Collections.Generic.IEnumerable%601> of <xref:System.Xml.Linq.XElement>, as shown in the example in this article.</span></span> <span data-ttu-id="77d6a-109">カスタムの軸メソッドでは、<xref:System.Xml.Linq.XNode.ReadFrom%2A> メソッドを呼び出して XML フラグメントを作成した後に、`yield return` を使用してコレクションを返します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-109">In the custom axis method, after you create the XML fragment by calling the <xref:System.Xml.Linq.XNode.ReadFrom%2A> method, return the collection using `yield return`.</span></span> <span data-ttu-id="77d6a-110">これにより、カスタムの軸メソッドに遅延実行セマンティクスが付加されます。</span><span class="sxs-lookup"><span data-stu-id="77d6a-110">This provides deferred execution semantics to your custom axis method.</span></span>

<span data-ttu-id="77d6a-111"><xref:System.Xml.XmlReader> オブジェクトから XML ツリーを作成する場合は、<xref:System.Xml.XmlReader> を要素に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="77d6a-111">When you create an XML tree from an <xref:System.Xml.XmlReader> object, the <xref:System.Xml.XmlReader> must be positioned on an element.</span></span> <span data-ttu-id="77d6a-112"><xref:System.Xml.Linq.XNode.ReadFrom%2A> メソッドは、要素の終了タグを読み取るまで制御を戻しません。</span><span class="sxs-lookup"><span data-stu-id="77d6a-112">The <xref:System.Xml.Linq.XNode.ReadFrom%2A> method doesn't return until it has read the close tag of the element.</span></span>

<span data-ttu-id="77d6a-113">部分ツリーを作成する場合は、<xref:System.Xml.XmlReader> をインスタンス化し、<xref:System.Xml.Linq.XElement> ツリーに変換するノード上にリーダーを配置し、<xref:System.Xml.Linq.XElement> オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-113">If you want to create a partial tree, you can instantiate an <xref:System.Xml.XmlReader>, position the reader on the node that you want to convert to an <xref:System.Xml.Linq.XElement> tree, and then create the <xref:System.Xml.Linq.XElement> object.</span></span>

<span data-ttu-id="77d6a-114">「[ヘッダー情報にアクセスして XML フラグメントをストリーム出力する方法](stream-xml-fragments-access-header-information.md)」という記事には、より複雑なドキュメントをストリーム出力する方法が記載されています。</span><span class="sxs-lookup"><span data-stu-id="77d6a-114">The article [How to stream XML fragments with access to header information](stream-xml-fragments-access-header-information.md) contains information on streaming a more complex document.</span></span>

<span data-ttu-id="77d6a-115">「[大きな XML ドキュメントのストリーミング変換を実行する方法](perform-streaming-transform-large-xml-documents.md)」という記事には、LINQ to XML を使用し、メモリ占有領域を低く抑えながら非常に大きな XML ドキュメントを変換する例が記載されています。</span><span class="sxs-lookup"><span data-stu-id="77d6a-115">The article [How to perform streaming transform of large XML documents](perform-streaming-transform-large-xml-documents.md) contains an example of using LINQ to XML to transform extremely large XML documents while maintaining a small memory footprint.</span></span>

## <a name="example-create-a-custom-axis-method"></a><span data-ttu-id="77d6a-116">例: カスタムの軸メソッドを作成する</span><span class="sxs-lookup"><span data-stu-id="77d6a-116">Example: Create a custom axis method</span></span>

<span data-ttu-id="77d6a-117">次の例では、カスタムの軸メソッドを作成します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-117">This example creates a custom axis method.</span></span> <span data-ttu-id="77d6a-118">このメソッドに対してクエリを実行するには、LINQ クエリを使用します。</span><span class="sxs-lookup"><span data-stu-id="77d6a-118">You can query it by using a LINQ query.</span></span> <span data-ttu-id="77d6a-119">カスタムの軸メソッド `StreamRootChildDoc` では、繰り返す `Child` 要素が含まれるドキュメントを読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="77d6a-119">The custom axis method `StreamRootChildDoc` can read a document that has a repeating `Child` element.</span></span>

```csharp
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)
{
    using (XmlReader reader = XmlReader.Create(stringReader))
    {
        reader.MoveToContent();
        // Parse the file and display each of the nodes.
        while (reader.Read())
        {
            switch (reader.NodeType)
            {
                case XmlNodeType.Element:
                    if (reader.Name == "Child") {
                        XElement el = XElement.ReadFrom(reader) as XElement;
                        if (el != null)
                            yield return el;
                    }
                    break;
            }
        }
    }
}

static void Main(string[] args)
{
    string markup = @"<Root>
      <Child Key=""01"">
        <GrandChild>aaa</GrandChild>
      </Child>
      <Child Key=""02"">
        <GrandChild>bbb</GrandChild>
      </Child>
      <Child Key=""03"">
        <GrandChild>ccc</GrandChild>
      </Child>
    </Root>";

    IEnumerable<string> grandChildData =
        from el in StreamRootChildDoc(new StringReader(markup))
        where (int)el.Attribute("Key") > 1
        select (string)el.Element("GrandChild");

    foreach (string str in grandChildData) {
        Console.WriteLine(str);
    }
}
```

```vb
Module Module1
    Sub Main()
        Dim markup = "<Root>" &
                     "  <Child Key=""01"">" &
                     "    <GrandChild>aaa</GrandChild>" &
                     "  </Child>" &
                     "  <Child Key=""02"">" &
                     "    <GrandChild>bbb</GrandChild>" &
                     "  </Child>" &
                     "  <Child Key=""03"">" &
                     "    <GrandChild>ccc</GrandChild>" &
                     "  </Child>" &
                     "</Root>"

        Dim grandChildData =
             From el In New StreamRootChildDoc(New IO.StringReader(markup))
             Where CInt(el.@Key) > 1
             Select el.<GrandChild>.Value

        For Each s In grandChildData
            Console.WriteLine(s)
        Next
    End Sub
End Module

Public Class StreamRootChildDoc
    Implements IEnumerable(Of XElement)

    Private _stringReader As IO.StringReader

    Public Sub New(ByVal stringReader As IO.StringReader)
        _stringReader = stringReader
    End Sub

    Public Function GetEnumerator() As IEnumerator(Of XElement) Implements IEnumerable(Of XElement).GetEnumerator
        Return New StreamChildEnumerator(_stringReader)
    End Function

    Public Function GetEnumerator1() As IEnumerator Implements IEnumerable.GetEnumerator
        Return Me.GetEnumerator()
    End Function
End Class

Public Class StreamChildEnumerator
    Implements IEnumerator(Of XElement)

    Private _current As XElement
    Private _reader As Xml.XmlReader
    Private _stringReader As IO.StringReader

    Public Sub New(ByVal stringReader As IO.StringReader)
        _stringReader = stringReader
        _reader = Xml.XmlReader.Create(_stringReader)
        _reader.MoveToContent()
    End Sub

    Public ReadOnly Property Current As XElement Implements IEnumerator(Of XElement).Current
        Get
            Return _current
        End Get
    End Property

    Public ReadOnly Property Current1 As Object Implements IEnumerator.Current
        Get
            Return Me.Current
        End Get
    End Property

    Public Function MoveNext() As Boolean Implements IEnumerator.MoveNext
        While _reader.Read()
            Select Case _reader.NodeType
                Case Xml.XmlNodeType.Element
                    Dim el = TryCast(XElement.ReadFrom(_reader), XElement)
                    If el IsNot Nothing Then
                        _current = el
                        Return True
                    End If
            End Select
        End While

        Return False
    End Function

    Public Sub Reset() Implements IEnumerator.Reset
        _reader = Xml.XmlReader.Create(_stringReader)
        _reader.MoveToContent()
    End Sub

#Region "IDisposable Support"

    Private disposedValue As Boolean ' To detect redundant calls

    ' IDisposable
    Protected Overridable Sub Dispose(ByVal disposing As Boolean)
        If Not Me.disposedValue Then
            If disposing Then
                _reader.Close()
            End If
        End If
        Me.disposedValue = True
    End Sub

    Public Sub Dispose() Implements IDisposable.Dispose
        Dispose(True)
        GC.SuppressFinalize(Me)
    End Sub
#End Region

End Class
```

<span data-ttu-id="77d6a-120">この例を実行すると、次の出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="77d6a-120">This example produces the following output:</span></span>

```output
bbb
ccc
```

<span data-ttu-id="77d6a-121">この例で使用されている手法では、`Child` 要素が大量にある場合でも、メモリ占有領域が少ない状態で維持されます。</span><span class="sxs-lookup"><span data-stu-id="77d6a-121">The technique used in this example maintains a small memory footprint even for millions of `Child` elements.</span></span>

## <a name="see-also"></a><span data-ttu-id="77d6a-122">関連項目</span><span class="sxs-lookup"><span data-stu-id="77d6a-122">See also</span></span>

- [<span data-ttu-id="77d6a-123">解析 XML</span><span class="sxs-lookup"><span data-stu-id="77d6a-123">Parse XML</span></span>](parse-string.md)
