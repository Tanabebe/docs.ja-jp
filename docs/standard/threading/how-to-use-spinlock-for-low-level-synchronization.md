---
description: '詳細情報: 下位レベルの同期に SpinLock を使用する方法'
title: '方法: 下位レベルの同期に SpinLock を使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to use
ms.assetid: a9ed3e4e-4f29-4207-b730-ed0a51ecbc19
ms.openlocfilehash: 854d34b94d04ea4817b7818193324b8dc4d0a44a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666746"
---
# <a name="how-to-use-spinlock-for-low-level-synchronization"></a>方法: 下位レベルの同期に SpinLock を使用する

<xref:System.Threading.SpinLock> の使用例を以下に示します。 この例では、クリティカル セクションが実行する作業量は最小限であるため、<xref:System.Threading.SpinLock> に適しています。 作業量を少し増やすと、標準ロックと比較して <xref:System.Threading.SpinLock> のパフォーマンスは高まります。 ただし、SpinLock が標準ロックよりも高負荷になるポイントがあります。 プロファイリング ツールでコンカレンシープロファイリング機能を使用して、どのタイプのロックを使用すればプログラムのパフォーマンスが高まるかを確認できます。 詳細については、「[コンカレンシー ビジュアライザー](/visualstudio/profiling/concurrency-visualizer)」を参照してください。  
  
 [!code-csharp[CDS_SpinLock#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#02)]
 [!code-vb[CDS_SpinLock#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_vb.vb#02)]  
  
 <xref:System.Threading.SpinLock> は、共有リソースのロックが非常に長い期間使用されない場合に有用なことがあります。 そのような場合、マルチコア コンピューターでは、ロックが解除されるまで数回のサイクルの間、ブロックされたスレッドをスピンさせると効率が高まることがあります。 スピンするとスレッドはブロックされなくなりますが、これは CPU 負荷の高いプロセスです。 ハイパースレッディングを使用するシステムでは、<xref:System.Threading.SpinLock> は特定の状況でスピンを停止して、論理プロセッサの不足や優先順位の逆転が発生するのを回避します。  
  
 この例では、<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> クラスを使用するため、マルチスレッド アクセスにはユーザーによる同期が必要になります。 別の選択肢としては <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType> を使用します。その場合、ユーザー ロックは不要です。  
  
 <xref:System.Threading.SpinLock.Exit%2A?displayProperty=nameWithType> の呼び出しに `false` が使用されていることに注目してください。 これにより、最適なパフォーマンスを得られます。 メモリ フェンスを使用するには、IA64 アーキテクチャで `true` を指定します。これにより、書き込みバッファーがフラッシュされるので、ロックを使用して他のスレッドを確実に入力できるようになります。
  
## <a name="see-also"></a>参照

- [スレッド処理オブジェクトと機能](threading-objects-and-features.md)
- [lock ステートメント (C#)](../../csharp/language-reference/keywords/lock-statement.md)
- [SyncLock ステートメント (Visual Basic)](../../visual-basic/language-reference/statements/synclock-statement.md)
