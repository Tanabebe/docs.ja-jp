---
description: '詳細情報: AssemblyAttributesGoHereS'
title: AssemblyAttributesGoHereS
ms.date: 03/30/2017
api_name:
- System.Runtime.CompilerServices.AssemblyAttributesGoHereS
api_location:
- mscorlib.dll
api_type:
- Assembly
f1_keywords:
- AssemblyAttributesGoHereS
helpviewer_keywords:
- AssemblyAttributesGoHereS type
- Alink API, AssemblyAttributesGoHereS type
ms.assetid: 4e817f35-a2bc-4403-9e6f-f731e6b9fe23
topic_type:
- apiref
ms.openlocfilehash: 7dad672a91375ee223ebb521b9e26ee280cf0531
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638562"
---
# <a name="assemblyattributesgoheres"></a><span data-ttu-id="172f3-103">AssemblyAttributesGoHereS</span><span class="sxs-lookup"><span data-stu-id="172f3-103">AssemblyAttributesGoHereS</span></span>

<span data-ttu-id="172f3-104">ALink でプレースホルダーとして使用し、カスタム属性に関する情報を格納します。</span><span class="sxs-lookup"><span data-stu-id="172f3-104">Used by ALink as a placeholder to store information about custom attributes.</span></span>

## <a name="syntax"></a><span data-ttu-id="172f3-105">構文</span><span class="sxs-lookup"><span data-stu-id="172f3-105">Syntax</span></span>

```csharp
internal sealed class AssemblyAttributesGoHereS
```

## <a name="remarks"></a><span data-ttu-id="172f3-106">解説</span><span class="sxs-lookup"><span data-stu-id="172f3-106">Remarks</span></span>

<span data-ttu-id="172f3-107">この型への参照は、ソースにアセンブリのカスタム属性が含まれている netmodule 内部に埋め込まれていることがあります。</span><span class="sxs-lookup"><span data-stu-id="172f3-107">References to this type might be embedded inside netmodules whose sources contain assembly custom attributes.</span></span> <span data-ttu-id="172f3-108">これらの型への参照が含まれる 1 つまたは複数の  netmodule からアセンブリ マニフェストを作成すると、ALink はこれらの参照にアタッチされた情報を使用して、実際のカスタム属性を生成します。</span><span class="sxs-lookup"><span data-stu-id="172f3-108">When building an assembly manifest from one or more netmodules that contain references to these types, ALink uses information attached to these references to emit real custom attributes.</span></span> <span data-ttu-id="172f3-109">このため、この型がインスタンス化されることはなく、その型への参照はビルド処理の一部としてのみ使用され、最終的なアセンブリでは使用されません。</span><span class="sxs-lookup"><span data-stu-id="172f3-109">As such, this type is never instantiated, and references to it are used only as part of the build process and serve no purpose in the final assembly.</span></span>

<span data-ttu-id="172f3-110">この型への参照は、セキュリティに関連せず複数の用途を持たないカスタム属性を示します。</span><span class="sxs-lookup"><span data-stu-id="172f3-110">References to this type indicate custom attributes that are security related and are not multiple-use.</span></span>

<span data-ttu-id="172f3-111">これらの型は .NET Framework 内で "内部的" とマーク付けされ、<xref:System.Runtime.CompilerServices> 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="172f3-111">These types are marked "internal" within the .NET Framework and are located in the <xref:System.Runtime.CompilerServices> namespace.</span></span>

## <a name="requirements"></a><span data-ttu-id="172f3-112">必要条件</span><span class="sxs-lookup"><span data-stu-id="172f3-112">Requirements</span></span>

<span data-ttu-id="172f3-113">mscorlib.dll</span><span class="sxs-lookup"><span data-stu-id="172f3-113">mscorlib.dll</span></span>

## <a name="see-also"></a><span data-ttu-id="172f3-114">関連項目</span><span class="sxs-lookup"><span data-stu-id="172f3-114">See also</span></span>

- [<span data-ttu-id="172f3-115">AssemblyAttributesGoHere</span><span class="sxs-lookup"><span data-stu-id="172f3-115">AssemblyAttributesGoHere</span></span>](assemblyattributesgohere.md)
- [<span data-ttu-id="172f3-116">AssemblyAttributesGoHereM</span><span class="sxs-lookup"><span data-stu-id="172f3-116">AssemblyAttributesGoHereM</span></span>](assemblyattributesgoherem.md)
- [<span data-ttu-id="172f3-117">AssemblyAttributesGoHereSM</span><span class="sxs-lookup"><span data-stu-id="172f3-117">AssemblyAttributesGoHereSM</span></span>](assemblyattributesgoheresm.md)
