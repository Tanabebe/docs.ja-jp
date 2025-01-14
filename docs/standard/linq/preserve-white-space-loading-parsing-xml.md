---
title: XML の読み込み時または解析時に空白を維持する - LINQ to XML
description: XML ツリーを設定する LINQ to XML メソッドの空白文字動作を制御できます。 たとえば、インメモリ処理のインデントを削除したり、そのままにしたりできます。
ms.date: 07/20/2015
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
ms.openlocfilehash: 783a1198f0b1754c690f04159860056a0fbadeb4
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "103411989"
---
# <a name="preserve-white-space-while-loading-or-parsing-xml-linq-to-xml"></a>XML の読み込み時または解析時に空白を維持する (LINQ to XML)

この記事では、空白に対する LINQ to XML の動作を制御する方法について説明します。

一般的なシナリオでは、インデントされた XML を読み取り、メモリ内に空白のテキスト ノードなしで (つまり空白を維持せずに) XML ツリーを作成し、XML に対して何らかの操作を実行し、インデント付きで XML を保存します。 書式を設定して XML をシリアル化する場合は、XML ツリー内の有意の空白のみが維持されます。 これが LINQ to XML の既定の動作です。

もう 1 つのよくあるシナリオは、意図的にインデントされた XML を読み取って変更する場合です。 場合によっては、このインデントを一切変更しないようにする必要があります。 LINQ to XML でこれを行うには、XML を読み込む際または解析する場合に空白を維持し、XML をシリアル化するときに書式設定を無効にします。

この記事では、空白に対する、XML ツリーを設定するメソッドの動作について説明します。 XML ツリーをシリアル化するときの空白の制御については、「[シリアル化時に空白を維持する](preserve-white-space-serializing.md)」を参照してください。

## <a name="behavior-of-methods-that-populate-xml-trees"></a>XML ツリーを設定するメソッドの動作

<xref:System.Xml.Linq.XElement> クラスと <xref:System.Xml.Linq.XDocument> クラスにある次のメソッドは、XML ツリーを設定します。 XML ツリーは、ファイル、<xref:System.IO.TextReader>、<xref:System.Xml.XmlReader>、または文字列から設定することができます。

- <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>
- <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>

メソッドが <xref:System.Xml.Linq.LoadOptions> を引数として受け取らない場合、意味のない空白は維持されません。

ほとんどの場合、メソッドが <xref:System.Xml.Linq.LoadOptions> を引数として受け取ると、意味のない空白を XML ツリー内のテキスト ノードとして維持できます。これは、オプションの動作です。 ただし、メソッドが <xref:System.Xml.XmlReader> から XML を読み込んでいる場合は、<xref:System.Xml.XmlReader> によって空白を維持するかどうかが決定されます。 <xref:System.Xml.Linq.LoadOptions.PreserveWhitespace> を設定しても効果はありません。

これらのメソッドで空白を維持すると、意味のない空白が <xref:System.Xml.Linq.XText> ノードとして XML ツリーに挿入されます。 空白が維持されない場合、テキスト ノードは挿入されません。

<xref:System.Xml.XmlWriter> を使用して、XML ツリーを作成することができます。 <xref:System.Xml.XmlWriter> に書き込まれたノードが、ツリーに挿入されます。 ただし、このメソッドを使用して XML ツリーを構築すると、ノードが空白かどうかにかかわらず、また空白に意味があるかどうかにかかわらず、すべてのノードが維持されます。
