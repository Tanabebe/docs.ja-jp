---
description: '詳細について: ICorProfilerInfo10:: RequestReJITWithInliners メソッド'
title: ICorProfilerInfo10::RequestReJITWithInliners
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo10.RequestReJITWithInliners
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: 925a61bf2521950cad7fb0dce8f1484198f3f806
ms.sourcegitcommit: 42d436ebc2a7ee02fc1848c7742bc7d80e13fc2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "102106515"
---
# <a name="icorprofilerinfo10requestrejitwithinliners-method"></a><span data-ttu-id="6a418-103">ICorProfilerInfo10:: RequestReJITWithInliners メソッド</span><span class="sxs-lookup"><span data-stu-id="6a418-103">ICorProfilerInfo10::RequestReJITWithInliners Method</span></span>

<span data-ttu-id="6a418-104">要求されたメソッドのほか、要求されたメソッドの inliners を再適用します。</span><span class="sxs-lookup"><span data-stu-id="6a418-104">ReJITs the methods requested, as well as any inliners of the methods requested.</span></span>

## <a name="syntax"></a><span data-ttu-id="6a418-105">構文</span><span class="sxs-lookup"><span data-stu-id="6a418-105">Syntax</span></span>

```cpp
HRESULT RequestReJITWithInliners( [in]                       DWORD       dwRejitFlags,
                                  [in]                       ULONG       cFunctions,
                                  [in, size_is(cFunctions)]  ModuleID    moduleIds[],
                                  [in, size_is(cFunctions)]  mdMethodDef methodIds[]);
```

## <a name="parameters"></a><span data-ttu-id="6a418-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="6a418-106">Parameters</span></span>

- `dwRejitFlags`

  <span data-ttu-id="6a418-107">\[in) [COR_PRF_REJIT_FLAGS](cor-prf-rejit-flags-enumeration.md)のビットマスク。</span><span class="sxs-lookup"><span data-stu-id="6a418-107">\[in] A bitmask of [COR_PRF_REJIT_FLAGS](cor-prf-rejit-flags-enumeration.md).</span></span>

- `cFunctions`

  <span data-ttu-id="6a418-108">\[in] 再コンパイルする関数の数。</span><span class="sxs-lookup"><span data-stu-id="6a418-108">\[in] The number of functions to recompile.</span></span>

- `moduleIds`

  <span data-ttu-id="6a418-109">\[in] は、再 `moduleId` `module` コンパイルする関数を識別する (、) ペアの部分を指定し `methodDef` ます。</span><span class="sxs-lookup"><span data-stu-id="6a418-109">\[in] Specifies the `moduleId` portion of the (`module`, `methodDef`) pairs that identify the functions to be recompiled.</span></span>

- `methodIds`

  <span data-ttu-id="6a418-110">\[in] は、再 `methodId` `module` コンパイルする関数を識別する (、) ペアの部分を指定し `methodDef` ます。</span><span class="sxs-lookup"><span data-stu-id="6a418-110">\[in] Specifies the `methodId` portion of the (`module`, `methodDef`) pairs that identify the functions to be recompiled.</span></span>

## <a name="remarks"></a><span data-ttu-id="6a418-111">解説</span><span class="sxs-lookup"><span data-stu-id="6a418-111">Remarks</span></span>

<span data-ttu-id="6a418-112">[RequestReJIT](icorprofilerinfo4-requestrejit-method.md) では、インラインメソッドの追跡は行われません。</span><span class="sxs-lookup"><span data-stu-id="6a418-112">[RequestReJIT](icorprofilerinfo4-requestrejit-method.md) does not do any tracking of inlined methods.</span></span> <span data-ttu-id="6a418-113">プロファイラーは、インライン化された `RequestReJIT` メソッドのすべてのインスタンスが ReJITted であることを確認するために、インライン展開をブロックするか、インライン展開を追跡し、すべての inliners に対してを呼び出す必要がありました</span><span class="sxs-lookup"><span data-stu-id="6a418-113">The profiler was expected to either block inlining or track inlining and call `RequestReJIT` for all inliners to make sure every instance of an inlined method was ReJITted.</span></span> <span data-ttu-id="6a418-114">これにより、再インライン化を監視するためのプロファイラーが存在しないため、ReJIT on attach に問題が生じます。</span><span class="sxs-lookup"><span data-stu-id="6a418-114">This poses a problem with ReJIT on attach, since the profiler is not present to monitor inlining.</span></span> <span data-ttu-id="6a418-115">このメソッドを呼び出すことにより、inliners の完全なセットも ReJITted になることを保証できます。</span><span class="sxs-lookup"><span data-stu-id="6a418-115">This method can be called to guarantee that the full set of inliners will be ReJITted as well.</span></span>

## <a name="requirements"></a><span data-ttu-id="6a418-116">必要条件</span><span class="sxs-lookup"><span data-stu-id="6a418-116">Requirements</span></span>

<span data-ttu-id="6a418-117">**プラットフォーム:** 「 [.Net Core でサポートされるオペレーティングシステム](../../../core/install/windows.md?pivots=os-windows)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6a418-117">**Platforms:** See [.NET Core supported operating systems](../../../core/install/windows.md?pivots=os-windows).</span></span>

<span data-ttu-id="6a418-118">**ヘッダー** : CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="6a418-118">**Header:** CorProf.idl, CorProf.h</span></span>

<span data-ttu-id="6a418-119">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6a418-119">**Library:** CorGuids.lib</span></span>

<span data-ttu-id="6a418-120">**.Net のバージョン:**[!INCLUDE[net_core_30](../../../../includes/net-core-30-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6a418-120">**.NET Versions:** [!INCLUDE[net_core_30](../../../../includes/net-core-30-md.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="6a418-121">関連項目</span><span class="sxs-lookup"><span data-stu-id="6a418-121">See also</span></span>

- [<span data-ttu-id="6a418-122">ICorProfilerInfo10 インターフェイス</span><span class="sxs-lookup"><span data-stu-id="6a418-122">ICorProfilerInfo10 Interface</span></span>](icorprofilerinfo10-interface.md)
