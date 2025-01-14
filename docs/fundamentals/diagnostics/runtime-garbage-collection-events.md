---
title: ガベージ コレクション ラインタイム イベント
description: .NET ガベージ コレクターに固有の診断情報を収集する .NET ランタイム イベントに関するページを参照してください。
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- GC events
- garbage collection events (CoreCLR)
- ETW, EventPipe, LTTng garbage collection events (CoreCLR)
ms.openlocfilehash: 2799a93f351baf23ec7a359b0b4b2be5c216dc4d
ms.sourcegitcommit: 05d0087dfca85aac9ca2960f86c5efd218bf833f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2021
ms.locfileid: "96594055"
---
# <a name="net-runtime-garbage-collection-events"></a>.NET ランタイム ガベージ コレクション イベント

これらのイベントは、ガベージ コレクションに関連する情報を収集します。 ガベージ コレクションが実行された回数、ガベージ コレクション中に解放されたメモリの量などの診断やデバッグに役立ちます。診断のためにこれらのイベントを使用する方法の詳細については、「[.NET Core のログとトレース](../../core/diagnostics/logging-tracing.md)」を参照してください。

## <a name="gcstart_v2-event"></a>GCStart_V2 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCStart_V1`|1|ガベージ コレクションが開始されました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*n* 回めのガベージ コレクション。|
|`Depth`|`win:UInt32`|収集されるジェネレーション。|
|`Reason`|`win:UInt32`|ガベージ コレクションが発生した理由:<br /><br /> `0x0` - 小さなオブジェクト ヒープの割り当て。<br /><br /> `0x1` - 強制実行。<br /><br /> `0x2` - メモリ不足。<br /><br /> `0x3` - 空。<br /><br /> `0x4` - 大きなオブジェクト ヒープの割り当て。<br /><br /> `0x5` - 領域不足 (小さなオブジェクト ヒープ対象)。<br /><br /> `0x6` - 領域不足 (大きなオブジェクト ヒープ対象)。<br /><br /> `0x7` - 強制実行されるが、ブロッキングとして強制されない。|
|`Type`|`win:UInt32`|`0x0` - バックグラウンド ガベージ コレクションの外部で発生するブロッキング ガベージ コレクション。<br /><br /> `0x1` - バックグラウンド ガベージ コレクション。<br /><br /> `0x2` - バックグラウンド ガベージ コレクションの実行中に発生するブロッキング ガベージ コレクション。|
|`ClrInstanceID`|win:UInt16|CoreCLR のインスタンスの一意の ID。|

## <a name="gcend_v1-event"></a>GCEnd_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCEnd_V1`|2|ガベージ コレクションが終了しました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*n* 回めのガベージ コレクション。|
|`Depth`|`win:UInt32`|収集されたジェネレーション。|
|`ClrInstanceID`|win:UInt16|CoreCLR のインスタンスの一意の ID。|

## <a name="gcheapstats_v2-event"></a>GCHeapStats_V2 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|説明|
|-----------|--------------|-----------------|
|`GCHeapStats_V2`|4|各ガベージ コレクション終了時のヒープの統計情報を示します。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`GenerationSize0`|`win:UInt64`|ジェネレーション 0 メモリのサイズ (バイト単位)。|
|`TotalPromotedSize0`|`win:UInt64`|ジェネレーション 0 からジェネレーション 1 に移されたバイト数。|
|`GenerationSize1`|`win:UInt64`|ジェネレーション 1 メモリのサイズ (バイト単位)。|
|`TotalPromotedSize1`|`win:UInt64`|ジェネレーション 1 からジェネレーション 2 に移されたバイト数。|
|`GenerationSize2`|`win:UInt64`|ジェネレーション 2 メモリのサイズ (バイト単位)。|
|`TotalPromotedSize2`|`win:UInt64`|最後のガベージ コレクションの後にジェネレーション 2 に残ったバイト数。|
|`GenerationSize3`|`win:UInt64`|大きなオブジェクト ヒープのサイズ (バイト単位)。|
|`TotalPromotedSize3`|`win:UInt64`|最後のガベージ コレクションの後に大きなオブジェクト ヒープに残ったバイト数。|
|`FinalizationPromotedSize`|`win:UInt64`|終了準備が完了しているオブジェクトの合計サイズ (バイト単位)。|
|`FinalizationPromotedCount`|`win:UInt64`|終了準備が完了しているオブジェクトの数。|
|`PinnedObjectCount`|`win:UInt32`|ピン止めオブジェクト (移動できないオブジェクト) の数。|
|`SinkBlockCount`|`win:UInt32`|使用中の同期ブロックの数。|
|`GCHandleCount`|`win:UInt32`|使用中のガベージ コレクション ハンドルの数。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|
|`GenerationSize4`|`win:UInt64`|固定オブジェクト ヒープのサイズ (バイト単位)。|
|`TotalPromotedSize4`|`win:UInt64`|最後のガベージ コレクションの後に固定オブジェクト ヒープに残ったバイト数。|

## <a name="gccreatesegment_v1-event"></a>GCCreateSegment_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCCreateSegment_V1`|5|新しいガベージ コレクション セグメントが作成されました。 既に実行されているプロセスでトレースを有効にした場合は、このイベントが各既存セグメントについて発生します。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|セグメントのアドレス。|
|`Size`|`win:UInt64`|セグメントのサイズ。|
|`Type`|`win:UInt32`|0x0 - 小さなオブジェクト ヒープ。<br /><br /> 0x1 - 大きなオブジェクト ヒープ。<br /><br /> 0x2 - 読み取り専用ヒープ。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

ガベージ コレクターによって割り当てられるセグメントのサイズは実装に固有であり、定期的な更新プログラムによる場合を含め、いつでも変更されることがあります。 アプリでは、セグメント サイズを推測することや、特定のセグメント サイズに依存することを絶対に避けてください。また、セグメントの割り当てに使用可能なメモリの量を構成しようとしてもなりません。

## <a name="gcfreesegment_v1-event"></a>GCFreeSegment_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCFreeSegment_V1`|6|ガベージ コレクション セグメントが解放されました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|セグメントのアドレス。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="gcrestarteebegin_v1-event"></a>GCRestartEEBegin_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCRestartEEBegin_V1`|7|共通言語ランタイムの中断からの再開が開始されました。|

このイベントには、イベント データはありません。

## <a name="gcrestarteeend_v1-event"></a>GCRestartEEEnd_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCRestartEEEnd_V1`|3|共通言語ランタイムの中断からの再開が終了しました。|

このイベントには、イベント データはありません。

## <a name="gcsuspendeeend_v1-event"></a>GCSuspendEEEnd_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCSuspendEEEnd_V1`|8|ガベージ コレクションのための実行エンジンの中断の終了。|

このイベントには、イベント データはありません。

## <a name="gcsuspendeebegin_v1-event"></a>GCSuspendEEBegin_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCSuspendEEBegin_V1`|8|ガベージ コレクションのための実行エンジンの中断の開始。|

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|*n* 回めのガベージ コレクション。|
|`Reason`|`win:UInt32`|EE の中断の理由。<br/><br/>`0x0`: その他の中断<br/><br/>`0x1`: GC による中断。<br/><br/>`0x2`: AppDomain のシャットダウンによる中断。<br/><br/>`0x3`: コード ピッチによる中断。<br/><br/>`0x4`: シャットダウンによる中断。<br/><br/>`0x5`: デバッガーによる中断。<br/><br/>`0x6`: GC 準備による中断。<br/><br/>`0x7`: デバッガー スイープによる中断|

## <a name="gcallocationtick_v3-event"></a>GCAllocationTick_V3 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|詳細 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCAllocationTick_V3`|10|約 100 KB が割り当てられるたび。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`AllocationAmount`|`win:UInt32`|割り当てサイズ (バイト単位)。 この値は、ULONG (4,294,967,295 バイト) の長さより短い割り当ての場合に正確です。 割り当てがこれを超える場合、このフィールドには切り捨てられた値が含まれます。 非常に大きな割り当てには `AllocationAmount64` を使用します。|
|`AllocationKind`|`win:UInt32`|`0x0` - 小さなオブジェクトの割り当て (小さなオブジェクト ヒープへの割り当て)。<br /><br /> `0x1` - 大きなオブジェクトの割り当て (大きなオブジェクト ヒープへの割り当て)。|
|`AllocationAmount64`|`win:UInt64`|割り当てサイズ (バイト単位)。 この値は非常に大きな割り当ての場合に正確です。|
|`TypeId`|`win:Pointer`|MethodTable のアドレス。 このイベント中に複数の型のオブジェクトが割り当てられた場合、これは最後に割り当てられたオブジェクト (100 KB のしきい値を超えたオブジェクト) に対応する MethodTable のアドレスです。|
|`TypeName`|`win:UnicodeString`|割り当てられた型の名前。 このイベント中に複数の型のオブジェクトが割り当てられた場合は、これは最後に割り当てられたオブジェクト (100 KB のしきい値を超えたオブジェクト) の型です。|
|`HeapIndex`|`win:UInt32`|オブジェクトが割り当てられたヒープ。 ワークステーションのガベージ コレクションと共に実行する場合、この値は 0 (ゼロ) になります。|
|`Address`|`win:Pointer`|最後に割り当てられたオブジェクトのアドレス。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="gccreateconcurrentthread_v1-event"></a>GCCreateConcurrentThread_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|
|`ThreadingKeyword` (0x10000)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCCreateConcurrentThread_V1`|11|同時実行ガベージ コレクション スレッドが作成されました。|

このイベントには、イベント データはありません。

## <a name="gcterminateconcurrentthread_v1-event"></a>GCTerminateConcurrentThread_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|
|`ThreadingKeyword` (0x10000)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCTerminateConcurrentThread_V1`|12|同時実行ガベージ コレクションスレッドが終了しました。|

このイベントには、イベント データはありません。

## <a name="gcfinalizersbegin_v1-event"></a>GCFinalizersBegin_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCFinalizersBegin_V1`|14|ファイナライザーの実行の開始。|

このイベントには、イベント データはありません。

## <a name="gcfinalizersend_v1-event"></a>GCFinalizersEnd_V1 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCFinalizersEnd_V1`|13|ファイナライザーの実行の終了。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|実行されたファイナライザーの数。|
|`ClrInstanceID`|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|

## <a name="setgchandle-event"></a>SetGCHandle イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCHandleKeyword` (0x2)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`SetGCHandle`|30|GC ハンドルが設定されました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|割り当てられたハンドルのアドレス。|
|`ObjectID`|`win:Pointer`|ハンドルが作成されたオブジェクトのアドレス。|
|`Kind`|`win:UInt32`|設定された GC ハンドルの型。 <br /><br />`0x0`: WeakShort <br/><br/>`0x1`: WeakLong <br /><br />`0x2`: Strong <br /><br />`0x3`: Pinned <br /><br />`0x4`: Variable<br /><br />`0x5`: RefCounted <br /><br />`0x6`: Dependent<br /><br />`0x7`: AsyncPinned<br /><br />`0x8`: SizedRef|
|`Generation`|`win:UInt32`|ハンドルが作成されたオブジェクトの世代。|
|`AppDomainID`|`win:UInt64`|AppDomain ID。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="destroygchandle-event"></a>DestroyGCHandle イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCHandleKeyword` (0x2)|情報提供 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`DestroyGCHandle`|31|GC ハンドルが破棄されます。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|破棄されたハンドルのアドレス。|
|`ClrInstanceID`|win:UInt16|CoreCLR のインスタンスの一意の ID。|

## <a name="pinobjectatgctime-event"></a>PinObjectAtGCTime イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|詳細 (5)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`PinObjectAtGCTime`|33|オブジェクトが GC 中に固定されました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|ハンドルのアドレス。|
|`ObjectID`|`win:Pointer`|固定オブジェクトのアドレス。|
|`ObjectSize`|`win:UInt64`|固定オブジェクトのサイズ。|
|`TypeName`|`win:UnicodeString`|固定オブジェクトの型の名前。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="gctriggered-event"></a>GCTriggered イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|詳細 (5)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCTriggered`|33|GC がトリガーされました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Reason`|`win:UInt32`|GC がトリガーされた理由。<br/><br/>`0x0`: AllocSmall<br/><br/>`0x1`: Induced <br/><br/>`0x2`: LowMemory <br/><br/>`0x3`: Empty <br/><br/>`0x4`: AllocLarge <br/><br/>`0x5`: OutOfSpaceSmallObjectHeap <br/><br/>`0x6`: OutOfSpaceLargeObjectHeap <br/><br/>`0x7`: InducedNoForce <br/><br/>`0x8`: Stress <br/><br/>`0x9`: InducedLowMemory|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="increasememorypressure-event"></a>IncreaseMemoryPressure イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|----------------|---------------|-----------------|
|`IncreaseMemoryPressure`|200|メモリの負荷が増加しました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`ClrInstanceID`|win:UInt16|CoreCLR のインスタンスの一意の ID。|

## <a name="decreasememorypressure-event"></a>DecreaseMemoryPressure イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|----------------|---------------|-----------------|
|`DecreaseMemoryPressure`|201|メモリの負荷が減少しました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`BytesFreed`|`win:UInt32`|解放されたバイト数。|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|

## <a name="gcmarkwithtype-event"></a>GCMarkWithType イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|情報 (4)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|----------------|---------------|-----------------|
|`GCMarkWithType`|202|GC マーク フェーズ中に GC ルートがマークされました。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`HeapNum`|`win:UInt32`|ヒープ番号。|
|`ClrInstanceID`|win:UInt16|CoreCLR のインスタンスの一意の ID。|
|`Type`|`win:UInt32`|GC ルート型。<br/><br/>`0x0`: Stack<br/><br/>`0x1`: Finalizer<br/><br/>`0x2`: Handle<br/><br/>`0x3`: Older<br/><br/>`0x4`: SizedRef<br/><br/>`0x5`: Overflow<br/><br/>|
|`Bytes`|`win:UInt64`|マークされたバイト数。|

## <a name="gcjoin_v2-event"></a>GCJoin_V2 イベント

次の表に、キーワードとレベルを示します。

|イベントを発生させるキーワード|Level|
|-----------------------------------|-----------|
|`GCKeyword` (0x1)|詳細 (5)|

次の表に、イベント情報を示します。

|Event|イベント ID|いつ発生するか|
|-----------|--------------|-----------------|
|`GCJoin_V2`|203|結合した GC スレッド。|

次の表に、イベント データを示します。

|フィールド名|データ型|説明|
|----------------|---------------|-----------------|
|`Heap`|`win:UInt32`|ヒープ番号|
|`JoinTime`|`win:UInt32`|このイベントが結合の開始時に発生したか、または結合の終了時に発生したかを示す (`0x0` は結合の開始、`0x1` は結合の終了)|
|`JoinType`|`win:UInt32`|結合の種類。 <br/><br/>`0x0`: 最後の結合<br/><br/>`0x1`: 結合 <br/><br/>`0x2`: 再起動 <br/><br/>`0x3`: 最初の逆結合<br/><br/>`0x4`: 逆結合<br/><br/>|
|`ClrInstanceID`|`win:UInt16`|CoreCLR のインスタンスの一意の ID。|
