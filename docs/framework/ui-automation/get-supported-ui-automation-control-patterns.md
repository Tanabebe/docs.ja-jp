---
title: サポートされている UI オートメーション コントロール パターンの取得
description: サポートされているコントロール パターン オブジェクトを UI オートメーション要素から取得する方法を示す例をご覧ください。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, getting
- UI Automation, getting control patterns
- getting, control patterns
ms.assetid: 006c54c9-50bf-48d9-a855-9d62eb95603a
ms.openlocfilehash: 68abe272e91c40932aba5bcf99394c4a8f815c53
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276452"
---
# <a name="get-supported-ui-automation-control-patterns"></a>サポートされている UI オートメーション コントロール パターンの取得

> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要素からコントロール パターン オブジェクトを取得する方法について説明します。  
  
### <a name="obtain-all-control-patterns"></a>すべてのコントロール パターンの取得  
  
1. 対象とするコントロール パターンを持つ <xref:System.Windows.Automation.AutomationElement> を取得します。  
  
2. 要素からすべてのコントロール パターンを取得するために、<xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> を呼び出します。  
  
> [!CAUTION]
> クライアントでは <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> を使用しないことを強くお勧めします。 このメソッドは内部で既存のコントロール パターンごとに <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> を呼び出すため、パフォーマンスに重大な影響を及ぼす可能性があります。 可能であれば、クライアントでは主なパターンに対して <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> を呼び出してください。  
  
### <a name="obtain-a-specific-control-pattern"></a>特定のコントロール パターンの取得  
  
1. 対象とするコントロール パターンを持つ <xref:System.Windows.Automation.AutomationElement> を取得します。  
  
2. 特定のパターンを照会するために、<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> または <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> を呼び出します。 これらのメソッドは同様ですが、パターンが見つからない場合、<xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> では例外が発生し、<xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> では `false` が返されます。  
  
## <a name="example"></a>例  

 次の例では、リスト項目の <xref:System.Windows.Automation.AutomationElement> を検索し、その要素から <xref:System.Windows.Automation.SelectionItemPattern> を取得します。  
  
 [!code-csharp[UIAClient_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#103)]
 [!code-vb[UIAClient_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#103)]  
  
## <a name="see-also"></a>関連項目

- [クライアントの UI オートメーション コントロール パターン](ui-automation-control-patterns-for-clients.md)
