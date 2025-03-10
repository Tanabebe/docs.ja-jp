---
title: 弱い参照
description: アプリケーションからオブジェクトへのアクセスを許容したまま、そのオブジェクトを .NET ガベージ コレクターが収集できるようにする、弱い参照について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- weak references, short
- weak references, using
- weak references, long
- garbage collection, weak references
ms.assetid: 6a600fe5-3af3-4c64-82da-10a0a8e2d79b
ms.openlocfilehash: a364435a5b0a480b0f6f70315e2d5465f61e6b5a
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794660"
---
# <a name="weak-references"></a>弱い参照

ガベージ コレクターでは、アプリケーションのコードがオブジェクトにアクセスできる間、そのアプリケーションで使用中のオブジェクトを収集することはできません。 アプリケーションには、オブジェクトへの強い参照があると考えられます。  
  
 弱い参照は、アプリケーションからオブジェクトへのアクセスを許容したまま、そのオブジェクトをガベージ コレクターが収集できるようにします。 弱い参照は、強い参照が存在しない場合に、オブジェクトが収集されるまでの不確定の期間中のみ有効です。 弱い参照を使用すると、該当オブジェクトが収集されるのを回避するため、アプリケーションで強い参照を取得できます。 ただし、強い参照が再確立される前に、ガベージ コレクターが最初にオブジェクトにアクセスするリスクが常にあります。  
  
 弱い参照は、多くのメモリを使用するが、ガベージ コレクションによって回収される場合、簡単に再作成できるオブジェクトに便利です。  
  
 Windows フォーム アプリケーションのツリー ビューに、複雑な階層形式のオプション選択がユーザーに示されているとします。 基になるデータが大きければ、ユーザーがアプリケーションで他の操作を行っている場合、ツリーをメモリ内に保持しても効果的ではありません。  
  
 ユーザーがアプリケーションの別の部分に切り替えている場合、<xref:System.WeakReference> クラスを使用して、ツリーへの弱い参照を作成し、すべての強い参照を破棄できます。 ユーザーがツリーに戻ると、アプリケーションはツリーへの強い参照を取得しようとします。成功した場合、ツリーの再作成は回避されます。  
  
 オブジェクトで弱い参照を確立するには、追跡されるオブジェクトのインスタンスを使用して、<xref:System.WeakReference> を作成します。 コード例については、クラス ライブラリの「<xref:System.WeakReference>」を参照してください。  
  
## <a name="short-and-long-weak-references"></a>短期間と長期間の弱い参照  

 短期間の弱い参照または長期間の弱い参照を作成できます。  
  
- Short  
  
     短期間の弱い参照の対象は、オブジェクトがガベージ コレクションによって回収されると、`null` になります。 弱い参照自体が管理オブジェクトであり、その他の管理オブジェクトと同じようにガベージ コレクションの対象です。  短期間の弱い参照は、<xref:System.WeakReference> のパラメーターなしのコンストラクターです。  
  
- Long  
  
     長期間の弱い参照は、オブジェクトの <xref:System.Object.Finalize%2A> メソッドが呼び出された後も保持されます。 これにより、オブジェクトが再作成されることを許可しますが、オブジェクトの状態は予測不可能なままです。 長い参照を使用するには、<xref:System.WeakReference> コンストラクターに `true` を指定します。  
  
     オブジェクトの型に <xref:System.Object.Finalize%2A> メソッドがない場合、短期間の弱い参照の機能が適用され、弱い参照はターゲットが収集されるまで有効です。これはファイナライザーを実行した後であれば、いつでも発生する可能性があります。  
  
 強い参照を確立して、もう一度オブジェクトを使用するには、オブジェクトの型に <xref:System.WeakReference> の <xref:System.WeakReference.Target%2A> プロパティをキャストします。 <xref:System.WeakReference.Target%2A> プロパティが `null` を返す場合、オブジェクトが収集されます。それ以外の場合、アプリケーションがその強い参照を再取得するため、オブジェクトを使用し続けることができます。  
  
## <a name="guidelines-for-using-weak-references"></a>弱い参照を使用するためのガイドライン  

 終了処理後のオブジェクトの状態が予測できないため、長期間の弱い参照は必要な場合にのみ使用します。  
  
 ポインター自体が同程度の大きさか、より大きい場合があるため、小さなオブジェクトへの弱い参照を使用しないでください。  
  
 メモリ管理の問題への自動的な解決方法として、弱い参照を使用しないでください。 代わりに、アプリケーションのオブジェクトを処理するために、効果的なキャッシュ ポリシーを開発します。  
  
## <a name="see-also"></a>関連項目

- [ガベージ コレクション](index.md)
