---
description: '詳細情報: ICorThreadpool::CorGetMaxThreads メソッド'
title: ICorThreadpool::CorGetMaxThreads メソッド
ms.date: 03/30/2017
api_name:
- ICorThreadpool.CorGetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorGetMaxThreads
helpviewer_keywords:
- CorGetMaxThreads method [.NET Framework hosting]
- ICorThreadpool::CorGetMaxThreads method [.NET Framework hosting]
ms.assetid: 2861533a-cda0-47b3-b716-0d363505289b
topic_type:
- apiref
ms.openlocfilehash: 44de36a7ff3e086ab9389049137c66697af11af3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99636469"
---
# <a name="icorthreadpoolcorgetmaxthreads-method"></a><span data-ttu-id="c5a25-103">ICorThreadpool::CorGetMaxThreads メソッド</span><span class="sxs-lookup"><span data-stu-id="c5a25-103">ICorThreadpool::CorGetMaxThreads Method</span></span>

<span data-ttu-id="c5a25-104">このメソッドは、.NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="c5a25-104">This method supports the .NET Framework infrastructure and is not intended to be used directly from your code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c5a25-105">構文</span><span class="sxs-lookup"><span data-stu-id="c5a25-105">Syntax</span></span>  
  
```cpp  
HRESULT CorGetMaxThreads (  
    [out] DWORD *MaxWorkerThreads,  
    [out] DWORD *MaxIOCompletionThreads  
);  
```  
  
## <a name="requirements"></a><span data-ttu-id="c5a25-106">必要条件</span><span class="sxs-lookup"><span data-stu-id="c5a25-106">Requirements</span></span>  

 <span data-ttu-id="c5a25-107">**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c5a25-107">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c5a25-108">**ヘッダー:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="c5a25-108">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="c5a25-109">**ライブラリ:** MSCorEE.dll にリソースとして含まれます</span><span class="sxs-lookup"><span data-stu-id="c5a25-109">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c5a25-110">**.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c5a25-110">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c5a25-111">関連項目</span><span class="sxs-lookup"><span data-stu-id="c5a25-111">See also</span></span>

- [<span data-ttu-id="c5a25-112">ICorThreadpool インターフェイス</span><span class="sxs-lookup"><span data-stu-id="c5a25-112">ICorThreadpool Interface</span></span>](icorthreadpool-interface.md)
