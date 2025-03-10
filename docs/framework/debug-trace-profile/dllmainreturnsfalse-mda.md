---
title: dllMainReturnsFalse MDA
description: .NET 内の dllMainReturnsFalse マネージド デバッグ アシスタントについて説明します。 この MDA は、DLL の初期化に失敗した場合にアクティブになります。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), DllMain returns false
- DllMainReturnsFalse MDA
- DllMain function
- MDAs (managed debugging assistants), DllMain returns false
ms.assetid: e2abdd04-f571-4b97-8c16-2221b8588429
ms.openlocfilehash: 83f38c4918c1354477627b70a62e60cbdc7de275
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273517"
---
# <a name="dllmainreturnsfalse-mda"></a>dllMainReturnsFalse MDA

`dllMainReturnsFalse` マネージド デバッグ アシスタント (MDA) は、DLL_PROCESS_ATTACH が原因で呼び出されたユーザー アセンブリのマネージド `DllMain` 関数が FALSE を返す場合にアクティブになります。  
  
## <a name="symptoms"></a>現象  

 `DllMain` 関数が、正しく実行されなかったことを示す FALSE を返しました。 `DllMain` 関数には通常、重要な初期化コードが含まれているため、これは原因不明の問題を引き起こす可能性があります。  
  
## <a name="cause"></a>原因  

 `DllMain` 関数は、ロード時の DLL 初期化の DLL_PROCESS_ATTACH が原因で呼び出されます。 FALSE が返された場合は、その DLL 初期化が失敗したことを意味します。  
  
## <a name="resolution"></a>解決方法  

 失敗した DLL の `DllMain` 関数のコードを分析し、初期化エラーの原因を特定します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  

 この MDA は CLR に影響しません。 `DllMain` の戻り値に関するデータのみを報告します。  
  
## <a name="output"></a>出力  

 DLL_PROCESS_ATTACH が原因で呼び出された `DllMain` 関数で FALSE が返されたことを示すメッセージ。 この MDA は、`DllMain` がマネージド コードで実装された場合にのみアクティブになることに注意してください。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dllMainReturnsFalse />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
