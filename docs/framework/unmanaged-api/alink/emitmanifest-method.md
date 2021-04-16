---
description: '詳細情報: EmitManifest メソッド'
title: EmitManifest メソッド
ms.date: 03/30/2017
api_name:
- EmitManifest
- IALink.EmitManifest
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EmitManifest
helpviewer_keywords:
- EmitManifest method
ms.assetid: fdebc1f3-b62e-4d9e-b775-8ccaa8ecb250
topic_type:
- apiref
ms.openlocfilehash: 770631864c030c067feb0b02d2f00c36076aa44c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638276"
---
# <a name="emitmanifest-method"></a><span data-ttu-id="0b6fa-103">EmitManifest メソッド</span><span class="sxs-lookup"><span data-stu-id="0b6fa-103">EmitManifest Method</span></span>

<span data-ttu-id="0b6fa-104">最終的なマニフェストを出力します。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-104">Emits the final manifest.</span></span> <span data-ttu-id="0b6fa-105">このメソッドは、他のすべてのファイルをインポートし、すべてのオプションを設定した後に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-105">Call this method after importing all other files and setting all options.</span></span> <span data-ttu-id="0b6fa-106">バインドされていないモジュールに対しては、このメソッドを呼び出さないでください。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-106">Do not call this method for unbound modules.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0b6fa-107">構文</span><span class="sxs-lookup"><span data-stu-id="0b6fa-107">Syntax</span></span>  
  
```cpp  
HRESULT EmitManifest(  
    mdAssembly   AssemblyID,  
    DWORD*       pdwReserveSize,  
    mdAssembly*  ptkManifest  
) PURE;  
```  
  
## <a name="parameters"></a><span data-ttu-id="0b6fa-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="0b6fa-108">Parameters</span></span>  

 `AssemblyID`  
 <span data-ttu-id="0b6fa-109">アセンブリの ID。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-109">ID of the assembly.</span></span>  
  
 `pdwReserveSize`  
 <span data-ttu-id="0b6fa-110">[StrongNameSignatureSize 関数](../strong-naming/strongnamesignaturesize-function.md)から取得した、アセンブリ ファイルで予約するサイズを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-110">Receives the size to reserve in the assembly file, retrieved from [StrongNameSignatureSize Function](../strong-naming/strongnamesignaturesize-function.md).</span></span>  
  
 `ptkManifest`  
 <span data-ttu-id="0b6fa-111">必要に応じて、アセンブリ マニフェスト トークンを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-111">Optionally receives the assembly manifest token.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="0b6fa-112">戻り値</span><span class="sxs-lookup"><span data-stu-id="0b6fa-112">Return Value</span></span>  

 <span data-ttu-id="0b6fa-113">メソッドが成功した場合は、S_OK が返されます。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-113">Returns S_OK if the method succeeds.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0b6fa-114">必要条件</span><span class="sxs-lookup"><span data-stu-id="0b6fa-114">Requirements</span></span>  

 <span data-ttu-id="0b6fa-115">alink.h を必要とします。</span><span class="sxs-lookup"><span data-stu-id="0b6fa-115">Requires alink.h.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0b6fa-116">関連項目</span><span class="sxs-lookup"><span data-stu-id="0b6fa-116">See also</span></span>

- [<span data-ttu-id="0b6fa-117">IALink インターフェイス</span><span class="sxs-lookup"><span data-stu-id="0b6fa-117">IALink Interface</span></span>](ialink-interface.md)
- [<span data-ttu-id="0b6fa-118">IALink2 インターフェイス</span><span class="sxs-lookup"><span data-stu-id="0b6fa-118">IALink2 Interface</span></span>](ialink2-interface.md)
- [<span data-ttu-id="0b6fa-119">ALink API</span><span class="sxs-lookup"><span data-stu-id="0b6fa-119">ALink API</span></span>](index.md)
