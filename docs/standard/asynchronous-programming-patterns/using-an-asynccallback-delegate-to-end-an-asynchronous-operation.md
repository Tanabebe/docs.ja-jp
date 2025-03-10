---
description: '詳細情報: AsyncCallback デリゲートの使用による非同期操作の終了'
title: AsyncCallback デリゲートの使用による非同期操作の終了
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ending asynchronous operations
- asynchronous programming, ending operations
- AsyncCallback delegate
- stopping asynchronous operations
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
ms.openlocfilehash: c97be1b9dbf225cfb76f8d9392269297fc1d123c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732190"
---
# <a name="using-an-asynccallback-delegate-to-end-an-asynchronous-operation"></a>AsyncCallback デリゲートの使用による非同期操作の終了

非同期操作の結果の待機中に、他の作業を実行できるアプリケーションは、操作が完了するまで待機をブロックする必要はありません。 次のオプションのいずれかを使用して、非同期操作が完了するまでの待機中に、手順の実行を継続します。  
  
- <xref:System.AsyncCallback> デリゲートを使用し、個別のスレッドで非同期操作の結果を処理します。 このトピックでは、この方法のデモが実行されます。  
  
- 非同期操作の **Begin**_OperationName_ メソッドによって返される <xref:System.IAsyncResult> の <xref:System.IAsyncResult.IsCompleted%2A> プロパティを使用して、その操作が完了したかどうかを判断します。 この方法のデモを実行する例については、「[非同期操作のステータスのポーリング](polling-for-the-status-of-an-asynchronous-operation.md)」を参照してください。  
  
## <a name="example"></a>例  

 次のコード例は、ユーザー指定のコンピューターのドメイン ネーム システム (DNS) 情報を取得するために、<xref:System.Net.Dns> クラスの非同期メソッドを使用してデモを実行します。 この例では、`ProcessDnsInformation` メソッドを参照する <xref:System.AsyncCallback> デリゲートを作成します。 このメソッドは、DNS 情報に対する非同期要求ごとに 1 回呼び出されます。  
  
 ユーザー指定のホストは、<xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.Object> パラメーターに渡されます。 複雑な状態オブジェクトの定義と使用に関するデモを実行する例については、「[AsyncCallback デリゲートおよび状態オブジェクトの使用](using-an-asynccallback-delegate-and-state-object.md)」を参照してください。  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [イベント ベースの非同期パターン (EAP)](event-based-asynchronous-pattern-eap.md)
- [イベントベースの非同期パターンの概要](event-based-asynchronous-pattern-overview.md)
- [IAsyncResult を使用した非同期メソッドの呼び出し](calling-asynchronous-methods-using-iasyncresult.md)
- [AsyncCallback デリゲートおよび状態オブジェクトの使用](using-an-asynccallback-delegate-and-state-object.md)
