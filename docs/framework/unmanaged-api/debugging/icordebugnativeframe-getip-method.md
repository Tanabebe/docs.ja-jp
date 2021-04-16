---
description: '詳細情報: ICorDebugNativeFrame::GetIP メソッド'
title: ICorDebugNativeFrame::GetIP メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
- ICorDebugNativeFrame::GetIP method [.NET Framework debugging]
ms.assetid: 99f693f3-d3b9-4fd8-9d09-b8efd03f7b67
topic_type:
- apiref
ms.openlocfilehash: f36a14c38aa6c3754cf78eca8c657adc76469067
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637836"
---
# <a name="icordebugnativeframegetip-method"></a><span data-ttu-id="278aa-103">ICorDebugNativeFrame::GetIP メソッド</span><span class="sxs-lookup"><span data-stu-id="278aa-103">ICorDebugNativeFrame::GetIP Method</span></span>

<span data-ttu-id="278aa-104">命令ポインターが現在設定されているネイティブ コードのオフセット位置を取得します。</span><span class="sxs-lookup"><span data-stu-id="278aa-104">Gets the native code offset location to which the instruction pointer is currently set.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="278aa-105">構文</span><span class="sxs-lookup"><span data-stu-id="278aa-105">Syntax</span></span>  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32           *pnOffset  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="278aa-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="278aa-106">Parameters</span></span>  

 `pnOffset`  
 <span data-ttu-id="278aa-107">[out] ネイティブ コード内のオフセット位置を指すポインター。</span><span class="sxs-lookup"><span data-stu-id="278aa-107">[out] A pointer to the offset location in the native code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="278aa-108">解説</span><span class="sxs-lookup"><span data-stu-id="278aa-108">Remarks</span></span>  

 <span data-ttu-id="278aa-109">この "ICorDebugNativeFrame" によって表されるスタック フレームがアクティブな場合、オフセットは次に実行される命令のアドレスになります。</span><span class="sxs-lookup"><span data-stu-id="278aa-109">If the stack frame that is represented by this "ICorDebugNativeFrame" is active, the offset is the address of the next instruction to be executed.</span></span> <span data-ttu-id="278aa-110">このスタック フレームがアクティブでない場合、オフセットは、スタック フレームが再アクティブ化されたときに実行される次の命令のアドレスになります。</span><span class="sxs-lookup"><span data-stu-id="278aa-110">If this stack frame is not active, the offset is the address of the next instruction to be executed when the stack frame is reactivated.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="278aa-111">必要条件</span><span class="sxs-lookup"><span data-stu-id="278aa-111">Requirements</span></span>  

 <span data-ttu-id="278aa-112">**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="278aa-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="278aa-113">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="278aa-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="278aa-114">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="278aa-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="278aa-115">**.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="278aa-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="278aa-116">関連項目</span><span class="sxs-lookup"><span data-stu-id="278aa-116">See also</span></span>
