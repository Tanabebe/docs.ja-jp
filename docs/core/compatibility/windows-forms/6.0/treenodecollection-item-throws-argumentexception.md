---
title: 破壊的変更:TreeNodeCollection.Item (Int32) から使用中のノードに対して ArgumentException がスローされる
description: 割り当て対象のノードが既に TreeView に割り当てられている場合、TreeNodeCollection.Item (Int32) から ArgumentException がスローされるようになったという、.NET 6 の破壊的変更について説明します。
ms.date: 01/19/2021
ms.openlocfilehash: 29727da2e4bc3d6ac89ed88819bf03d058603f77
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2021
ms.locfileid: "102255694"
---
# <a name="treenodecollectionitem-throws-exception-if-node-is-assigned-elsewhere"></a><span data-ttu-id="f652f-103">ノードが別のものに割り当てられている場合、TreeNodeCollection.Item により例外がスローされる</span><span class="sxs-lookup"><span data-stu-id="f652f-103">TreeNodeCollection.Item throws exception if node is assigned elsewhere</span></span>

<span data-ttu-id="f652f-104">割り当て対象のノードが、別の <xref:System.Windows.Forms.TreeView> に、または別のインデックスでこの <xref:System.Windows.Forms.TreeView> に既にバインドされている場合、<xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> から <xref:System.ArgumentException> がスローされます。</span><span class="sxs-lookup"><span data-stu-id="f652f-104"><xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> throws an <xref:System.ArgumentException> if the node being assigned is already bound to another <xref:System.Windows.Forms.TreeView> or to this <xref:System.Windows.Forms.TreeView> at a different index.</span></span>

## <a name="change-description"></a><span data-ttu-id="f652f-105">変更内容</span><span class="sxs-lookup"><span data-stu-id="f652f-105">Change description</span></span>

<span data-ttu-id="f652f-106">以前の .NET バージョンでは、ツリー ノードが既に <xref:System.Windows.Forms.TreeView> にバインドされている場合でも、コレクションにツリー ノードを割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="f652f-106">In previous .NET versions, you can assign a tree node to a collection even if it's already bound to a <xref:System.Windows.Forms.TreeView>.</span></span> <span data-ttu-id="f652f-107">これにより、重複するノードが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f652f-107">This can lead to duplicated nodes.</span></span> <span data-ttu-id="f652f-108">.NET 6 以降、割り当て対象のノードが、別の <xref:System.Windows.Forms.TreeView> に、または別のインデックスでこの <xref:System.Windows.Forms.TreeView> に既にバインドされている場合、<xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> から <xref:System.ArgumentException> がスローされます。</span><span class="sxs-lookup"><span data-stu-id="f652f-108">Starting in .NET 6, <xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=nameWithType> throws an <xref:System.ArgumentException> if the node being assigned is already bound to another <xref:System.Windows.Forms.TreeView> or to this <xref:System.Windows.Forms.TreeView> at a different index.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="f652f-109">変更理由</span><span class="sxs-lookup"><span data-stu-id="f652f-109">Reason for change</span></span>

<span data-ttu-id="f652f-110">入力パラメーターの検証を、他の `TreeNodeCollection` API の動作と同じにします。</span><span class="sxs-lookup"><span data-stu-id="f652f-110">Validating the input parameter is consistent with the behavior of other `TreeNodeCollection` APIs.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="f652f-111">導入されたバージョン</span><span class="sxs-lookup"><span data-stu-id="f652f-111">Version introduced</span></span>

<span data-ttu-id="f652f-112">.NET 6 Preview 1</span><span class="sxs-lookup"><span data-stu-id="f652f-112">.NET 6 Preview 1</span></span>

## <a name="recommended-action"></a><span data-ttu-id="f652f-113">推奨アクション</span><span class="sxs-lookup"><span data-stu-id="f652f-113">Recommended action</span></span>

<span data-ttu-id="f652f-114">コレクションに割り当てる前に、必ず `TreeNode` のバインドを解除します。</span><span class="sxs-lookup"><span data-stu-id="f652f-114">Make sure to unbind a `TreeNode` before assigning it to the collection.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="f652f-115">影響を受ける API</span><span class="sxs-lookup"><span data-stu-id="f652f-115">Affected APIs</span></span>

<xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)`

### Category

Windows Forms

-->
