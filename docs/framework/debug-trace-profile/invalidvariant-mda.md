---
title: invalidVariant MDA
description: invalidVariant マネージド デバッグ アシスタントについて確認します。これは、ネイティブ/アンマネージドからマネージ ドコードへの呼び出しで無効な VARIANT が検出された場合に呼び出されます。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid variant
- VARIANT type errors
- InvalidVariant MDA
- invalid VARIANT types
- managed debugging assistants (MDAs), invalid variant
ms.assetid: d273e070-d1b1-4a53-a9c7-7af837b04a3d
ms.openlocfilehash: f0667a54e950ead27000eb6b93ebd547dea1cfb0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96281301"
---
# <a name="invalidvariant-mda"></a>invalidVariant MDA

`invalidVariant` マネージド デバッグ アシスタント (MDA: Managed Debugging Assistant) は、ネイティブ コードまたはアンマネージド コードからマネージド コードへの呼び出し時に、無効な `VARIANT` 構造体が見つかるとアクティブ化されます。  
  
## <a name="symptoms"></a>現象  

 `VARIANT` からオブジェクトへのマーシャリングを含む、ネイティブ コードとマネージド コードの間の遷移中に、予期しない動作が発生します。  
  
## <a name="cause"></a>原因  

 ネイティブ コードが、不適切な `VARIANT` 構造体をマネージド コードに渡しています。  ランタイムは、この `VARIANT` をオブジェクトにマーシャリングしようとし、`VARIANT` が有効でない場合に MDA がアクティブ化されます。 無効な `VARIANT` には、`VARTYPE` VT_EMPTY &#124; VT_BYREF の `VARIANT` や、`VARTYPE` VT_VARIANT の `VARIANT` などがあります。  
  
## <a name="resolution"></a>解決方法  

 `VARIANT` を渡すネイティブ コードまたはアンマネージ コードでは、`VARIANT` の形式と初期化が正しいことを確認する必要があります。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  

 この MDA は、ランタイムの動作への影響はありません。  
  
## <a name="output"></a>出力  

 無効な `VARIANT` がアンマネージド モジュールによりマネージド コードに渡されたことを、ランタイムが検出したことを示す MDA メッセージです。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidVariant />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../interop/interop-marshaling.md)
