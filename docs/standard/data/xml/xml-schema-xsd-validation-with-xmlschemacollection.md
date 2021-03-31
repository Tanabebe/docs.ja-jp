---
description: '詳細情報: XmlSchemaCollection を使用した XML スキーマ (XSD) 検証'
title: XmlSchemaCollection を使用した XML スキーマ (XSD) 検証
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ad0b5717-3d32-41ad-a4d7-072c3e492b82
ms.openlocfilehash: b0363f6d5f656591d56a1202f223ee9797abd26d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782690"
---
# <a name="xml-schema-xsd-validation-with-xmlschemacollection"></a><span data-ttu-id="084c9-103">XmlSchemaCollection を使用した XML スキーマ (XSD) 検証</span><span class="sxs-lookup"><span data-stu-id="084c9-103">XML Schema (XSD) Validation with XmlSchemaCollection</span></span>

<span data-ttu-id="084c9-104"><xref:System.Xml.Schema.XmlSchemaCollection> を使用して、XML スキーマ定義言語 (XSD) スキーマを基準として XML ドキュメントを検証できます。</span><span class="sxs-lookup"><span data-stu-id="084c9-104">You can use the <xref:System.Xml.Schema.XmlSchemaCollection> to validate an XML document against XML Schema definition language (XSD) schemas.</span></span> <span data-ttu-id="084c9-105"><xref:System.Xml.Schema.XmlSchemaCollection> は、検証を行うたびにスキーマをメモリに読み込まなくてもいいように、スキーマをコレクションに格納することによってパフォーマンスの向上を図ります。</span><span class="sxs-lookup"><span data-stu-id="084c9-105">The <xref:System.Xml.Schema.XmlSchemaCollection> improves performance by storing schemas in the collection so they are not loaded into memory each time validation occurs.</span></span> <span data-ttu-id="084c9-106">スキーマがスキーマ コレクション内にある場合、コレクション内のスキーマの位置を特定するには `schemaLocation` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="084c9-106">If the schema exists in the schema collection, the `schemaLocation` attribute is used to look up the schema in the collection.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="084c9-107"><xref:System.Xml.Schema.XmlSchemaCollection> クラスは廃止されており、<xref:System.Xml.Schema.XmlSchemaSet> クラスに置き換えられています。</span><span class="sxs-lookup"><span data-stu-id="084c9-107">The <xref:System.Xml.Schema.XmlSchemaCollection> class is now obsolete and has been replaced with the <xref:System.Xml.Schema.XmlSchemaSet> class.</span></span> <span data-ttu-id="084c9-108"><xref:System.Xml.Schema.XmlSchemaSet> クラスの詳細については、「[スキーマをコンパイルするための XmlSchemaSet](xmlschemaset-for-schema-compilation.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="084c9-108">For more information about the <xref:System.Xml.Schema.XmlSchemaSet> class see, [XmlSchemaSet for Schema Compilation](xmlschemaset-for-schema-compilation.md).</span></span>  
  
 <span data-ttu-id="084c9-109">データ ファイルのルート要素の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-109">The following example shows the root element of a data file.</span></span>  
  
```xml  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns="urn:bookstore-schema"  
    elementFormDefault="qualified"  
    targetNamespace="urn:bookstore-schema">  
```  
  
 <span data-ttu-id="084c9-110">この例では、`targetNamespace` 属性の値として、スキーマを `urn:bookstore-schema` に追加するときに使用される名前空間と同じ <xref:System.Xml.Schema.XmlSchemaCollection> が指定されています。</span><span class="sxs-lookup"><span data-stu-id="084c9-110">For this example, the value of the `targetNamespace` attribute is `urn:bookstore-schema`, which is the same namespace that is used when adding the schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span>  
  
 <span data-ttu-id="084c9-111">XML スキーマを <xref:System.Xml.Schema.XmlSchemaCollection> に追加するコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-111">The following code example adds an XML Schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span>  
  
```vb  
Dim xsc As New XmlSchemaCollection()  
' XML Schema.  
xsc.Add("urn:bookstore-schema", schema)
reader = New XmlTextReader(filename)  
vreader = New XmlValidatingReader(reader)  
vreader.Schemas.Add(xsc)  
```  
  
```csharp  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
// XML Schema.  
xsc.Add("urn:bookstore-schema", schema);  
reader = new XmlTextReader (filename);  
vreader = new XmlValidatingReader (reader);  
vreader.Schemas.Add(xsc);  
```  
  
 <span data-ttu-id="084c9-112">`targetNamespace` の `namespaceURI` メソッドで <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> プロパティを追加する場合、一般的に、<xref:System.Xml.Schema.XmlSchemaCollection> 属性が使用されます。</span><span class="sxs-lookup"><span data-stu-id="084c9-112">The `targetNamespace` attribute is generally used when you add the `namespaceURI` property in the <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> method for the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span> <span data-ttu-id="084c9-113">スキーマを <xref:System.Xml.Schema.XmlSchemaCollection> に追加する前に、null 参照を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="084c9-113">You can specify a null reference before adding the schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span> <span data-ttu-id="084c9-114">名前空間が関連付けられていないスキーマに対しては、空の文字列 ("") を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="084c9-114">An empty string ("") should be used for schemas without a namespace.</span></span> <span data-ttu-id="084c9-115"><xref:System.Xml.Schema.XmlSchemaCollection> には、名前空間が関連付けられていないスキーマを 1 つだけ含めることができます。</span><span class="sxs-lookup"><span data-stu-id="084c9-115">The <xref:System.Xml.Schema.XmlSchemaCollection> can have only one schema without a namespace.</span></span>  
  
 <span data-ttu-id="084c9-116">XML スキーマ HeadCount.xsd を <xref:System.Xml.Schema.XmlSchemaCollection> に追加し、HeadCount.xml を検証するコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-116">The following code example adds an XML Schema, HeadCount.xsd, to the <xref:System.Xml.Schema.XmlSchemaCollection> and validates HeadCount.xml.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Schema  
  
Namespace ValidationSample  
  
   Class Sample  
  
      Public Shared Sub Main()  
         Dim tr As New XmlTextReader("HeadCount.xml")  
         Dim vr As New XmlValidatingReader(tr)  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd")  
         vr.ValidationType = ValidationType.Schema  
         AddHandler vr.ValidationEventHandler, AddressOf ValidationHandler  
  
         While vr.Read()  
         End While  
         Console.WriteLine("Validation finished")  
      End Sub  
      ' Main  
  
      Public Shared Sub ValidationHandler(sender As Object, args As ValidationEventArgs)  
         Console.WriteLine("***Validation error")  
         Console.WriteLine("Severity:{0}", args.Severity)  
         Console.WriteLine("Message:{0}", args.Message)  
      End Sub  
      ' ValidationHandler  
   End Class  
   ' Sample  
End Namespace  
' ValidationSample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Schema;  
  
namespace ValidationSample  
{  
   class Sample  
   {  
      public static void Main()  
      {  
         XmlTextReader tr = new XmlTextReader("HeadCount.xml");  
         XmlValidatingReader vr = new XmlValidatingReader(tr);  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd");  
         vr.ValidationType = ValidationType.Schema;  
         vr.ValidationEventHandler += new ValidationEventHandler (ValidationHandler);  
  
         while(vr.Read());  
         Console.WriteLine("Validation finished");  
      }  
  
      public static void ValidationHandler(object sender, ValidationEventArgs args)  
      {  
         Console.WriteLine("***Validation error");  
         Console.WriteLine("\tSeverity:{0}", args.Severity);  
         Console.WriteLine("\tMessage  :{0}", args.Message);  
      }  
   }  
}  
```  
  
 <span data-ttu-id="084c9-117">検証対象の入力ファイル HeadCount.xml の内容について、次に概略を示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-117">The following outlines the contents of the input file, HeadCount.xml, to be validated.</span></span>  
  
```xml  
<!--Load HeadCount.xsd in SchemaCollection for Validation-->  
<hc:HeadCount xmlns:hc='xsdHeadCount'>  
   <Name>Waldo Pepper</Name>  
   <Name>Red Pepper</Name>  
</hc:HeadCount>  
```  
  
 <span data-ttu-id="084c9-118">検証の基準とする XML スキーマ ファイル HeadCount.xsd の内容について、次に概略を示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-118">The following outlines the contents of the XML Schema file, HeadCount.xsd, to be validated against.</span></span>  
  
```xml  
<xs:schema xmlns="xsdHeadCount" targetNamespace="xsdHeadCount" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name='HeadCount' type="HEADCOUNT"/>  
   <xs:complexType name="HEADCOUNT">  
      <xs:sequence>  
         <xs:element name='Name' type='xs:string' maxOccurs='unbounded'/>  
      </xs:sequence>  
      <xs:attribute name='division' type='xs:int' use='optional' default='8'/>  
   </xs:complexType>  
</xs:schema>  
```  
  
 <span data-ttu-id="084c9-119"><xref:System.Xml.XmlValidatingReader> を受け取る <xref:System.Xml.XmlTextReader> を作成するコード サンプルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-119">The following code example creates an <xref:System.Xml.XmlValidatingReader> that takes an <xref:System.Xml.XmlTextReader>.</span></span> <span data-ttu-id="084c9-120">XML スキーマ sample4.xsd を基準として、入力ファイル sample4.xml を検証します。</span><span class="sxs-lookup"><span data-stu-id="084c9-120">The input file, sample4.xml, is validated against the XML Schema, sample4.xsd.</span></span>  
  
```vb  
Dim tr As New XmlTextReader("sample4.xml")  
Dim vr As New XmlValidatingReader(tr)  
vr.ValidationType = ValidationType.Schema  
vr.Schemas.Add("datatypesTest", "sample4.xsd")  
AddHandler vr.ValidationEventHandler, AddressOf ValidationCallBack  
While vr.Read()  
   Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name)  
End While  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("sample4.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
vr.ValidationType = ValidationType.Schema;  
        vr.Schemas.Add("datatypesTest", "sample4.xsd");  
vr.ValidationEventHandler += new ValidationEventHandler(ValidationCallBack);  
while(vr.Read()) {  
    Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name);  
    }  
```  
  
 <span data-ttu-id="084c9-121">検証対象とする入力ファイル sample4.xml の内容について、次に概略を示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-121">The following outlines the contents of the input file, sample4.xml, to be validated.</span></span>  
  
```xml  
<datatypes xmlns="datatypesTest">  
    <number>  
        <number_1>123</number_1>  
    </number>  
</datatypes>  
```  
  
 <span data-ttu-id="084c9-122">検証の基準とする XML スキーマ ファイル sample4.xsd の内容について、次に概略を示します。</span><span class="sxs-lookup"><span data-stu-id="084c9-122">The following outlines the contents of the XML Schema file, sample4.xsd, to be validated against.</span></span>  
  
```xml  
<xs:schema
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:tns="datatypesTest"
    targetNamespace="datatypesTest"  
    elementFormDefault="qualified">  
  
<xs:element name = "datatypes">  
  <xs:complexType>  
    <xs:all>  
        <xs:element name="number">  
            <xs:complexType>  
                <xs:sequence>  
                    <xs:element name="number_1" type="xs:decimal" maxOccurs="unbounded"/>  
                </xs:sequence>  
            </xs:complexType>  
        </xs:element>  
    </xs:all>  
  </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a><span data-ttu-id="084c9-123">関連項目</span><span class="sxs-lookup"><span data-stu-id="084c9-123">See also</span></span>

- <xref:System.Xml.XmlParserContext>
- <xref:System.Xml.XmlValidatingReader.ValidationEventHandler?displayProperty=nameWithType>
- <xref:System.Xml.XmlValidatingReader.Schemas%2A?displayProperty=nameWithType>
- [<span data-ttu-id="084c9-124">XmlSchemaCollection スキーマのコンパイル</span><span class="sxs-lookup"><span data-stu-id="084c9-124">XmlSchemaCollection Schema Compilation</span></span>](xmlschemacollection-schema-compilation.md)
