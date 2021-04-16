---
description: '詳細情報: ICLROnEventManager::RegisterActionOnEvent メソッド'
title: ICLROnEventManager::RegisterActionOnEvent メソッド
ms.date: 03/30/2017
api_name:
- ICLROnEventManager.RegisterActionOnEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLROnEventManager::RegisterActionOnEvent
helpviewer_keywords:
- ICLROnEventManager::RegisterActionOnEvent method [.NET Framework hosting]
- RegisterActionOnEvent method [.NET Framework hosting]
ms.assetid: b944cf49-918d-4c4e-993b-77d097a52550
topic_type:
- apiref
ms.openlocfilehash: b13209aed6a169185b42c6b9520f21f59f6be3bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637431"
---
# <a name="iclroneventmanagerregisteractiononevent-method"></a><span data-ttu-id="9166d-103">ICLROnEventManager::RegisterActionOnEvent メソッド</span><span class="sxs-lookup"><span data-stu-id="9166d-103">ICLROnEventManager::RegisterActionOnEvent Method</span></span>

<span data-ttu-id="9166d-104">指定したイベントのコールバック ポインターを登録します。</span><span class="sxs-lookup"><span data-stu-id="9166d-104">Registers a callback pointer for the specified event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9166d-105">構文</span><span class="sxs-lookup"><span data-stu-id="9166d-105">Syntax</span></span>  
  
```cpp  
HRESULT RegisterActionOnEvent (  
    [in] EClrEvent event,  
    [in] IActionOnCLREvent *pAction  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9166d-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="9166d-106">Parameters</span></span>  

 `event`  
 <span data-ttu-id="9166d-107">[in] [EClrEvent](eclrevent-enumeration.md) 値の 1 つ。`pAction` によって記述されたコールバック ポインターを登録するイベントを示します。</span><span class="sxs-lookup"><span data-stu-id="9166d-107">[in] One of the [EClrEvent](eclrevent-enumeration.md) values, indicating the event for which to register the callback pointer described by `pAction`.</span></span>  
  
 `pAction`  
 <span data-ttu-id="9166d-108">[in] 登録されたイベントが発生したときに呼び出される [IActionOnCLREvent](iactiononclrevent-interface.md) オブジェクトへのポインター。</span><span class="sxs-lookup"><span data-stu-id="9166d-108">[in] A pointer to an [IActionOnCLREvent](iactiononclrevent-interface.md) object that is called when the registered event fires.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="9166d-109">戻り値</span><span class="sxs-lookup"><span data-stu-id="9166d-109">Return Value</span></span>  
  
|<span data-ttu-id="9166d-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="9166d-110">HRESULT</span></span>|<span data-ttu-id="9166d-111">説明</span><span class="sxs-lookup"><span data-stu-id="9166d-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="9166d-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="9166d-112">S_OK</span></span>|<span data-ttu-id="9166d-113">`RegisterActionOnEvent` が正常に返されました。</span><span class="sxs-lookup"><span data-stu-id="9166d-113">`RegisterActionOnEvent` returned successfully.</span></span>|  
|<span data-ttu-id="9166d-114">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="9166d-114">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="9166d-115">共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージド コードを実行できないまたは呼び出しを正常に処理できない状態です。</span><span class="sxs-lookup"><span data-stu-id="9166d-115">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="9166d-116">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="9166d-116">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="9166d-117">呼び出しがタイムアウトしました。</span><span class="sxs-lookup"><span data-stu-id="9166d-117">The call timed out.</span></span>|  
|<span data-ttu-id="9166d-118">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="9166d-118">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="9166d-119">呼び出し元はロックを所有していません。</span><span class="sxs-lookup"><span data-stu-id="9166d-119">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="9166d-120">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="9166d-120">HOST_E_ABANDONED</span></span>|<span data-ttu-id="9166d-121">ブロックされたスレッドまたはファイバーが待機しているイベントがキャンセルされました。</span><span class="sxs-lookup"><span data-stu-id="9166d-121">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="9166d-122">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="9166d-122">E_FAIL</span></span>|<span data-ttu-id="9166d-123">不明な壊滅的なエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="9166d-123">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="9166d-124">メソッドにより E_FAIL が返された後、そのプロセス内で CLR が使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="9166d-124">After a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="9166d-125">ホスト メソッドに対する後続の呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。</span><span class="sxs-lookup"><span data-stu-id="9166d-125">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9166d-126">解説</span><span class="sxs-lookup"><span data-stu-id="9166d-126">Remarks</span></span>  

 <span data-ttu-id="9166d-127">ホストでは、`EClrEvent` によって記述された 2 つのイベントの種類のいずれか、または両方のコールバックを登録できます。</span><span class="sxs-lookup"><span data-stu-id="9166d-127">The host can register callbacks for either or both of the two event types described by `EClrEvent`.</span></span> <span data-ttu-id="9166d-128">ホストでは、[ICLRControl::GetCLRManager](iclrcontrol-getclrmanager-method.md) メソッドを呼び出すことで、`ICLROnEventManager` インターフェイスが取得されます。</span><span class="sxs-lookup"><span data-stu-id="9166d-128">The host gets the `ICLROnEventManager` interface by calling the [ICLRControl::GetCLRManager](iclrcontrol-getclrmanager-method.md) method.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9166d-129">`RegisterActionOnEvent` によって登録されるイベントをさまざまなスレッドから複数回起動すると、CLR のアンロードや無効化を通知できます。</span><span class="sxs-lookup"><span data-stu-id="9166d-129">The events that `RegisterActionOnEvent` registers can be fired more than once and from different threads to signal an unload or the disabling of the CLR.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9166d-130">必要条件</span><span class="sxs-lookup"><span data-stu-id="9166d-130">Requirements</span></span>  

 <span data-ttu-id="9166d-131">**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9166d-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9166d-132">**ヘッダー:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="9166d-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="9166d-133">**ライブラリ:** リソースとして MSCorEE.dll に含まれている</span><span class="sxs-lookup"><span data-stu-id="9166d-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="9166d-134">**.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9166d-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9166d-135">関連項目</span><span class="sxs-lookup"><span data-stu-id="9166d-135">See also</span></span>

- [<span data-ttu-id="9166d-136">EClrEvent 列挙型</span><span class="sxs-lookup"><span data-stu-id="9166d-136">EClrEvent Enumeration</span></span>](eclrevent-enumeration.md)
- [<span data-ttu-id="9166d-137">IActionOnCLREvent インターフェイス</span><span class="sxs-lookup"><span data-stu-id="9166d-137">IActionOnCLREvent Interface</span></span>](iactiononclrevent-interface.md)
- [<span data-ttu-id="9166d-138">ICLRControl インターフェイス</span><span class="sxs-lookup"><span data-stu-id="9166d-138">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="9166d-139">ICLROnEventManager インターフェイス</span><span class="sxs-lookup"><span data-stu-id="9166d-139">ICLROnEventManager Interface</span></span>](iclroneventmanager-interface.md)
