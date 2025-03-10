---
title: dirtyCastAndCallOnInterface MDA
description: dirtyCastAndCallOnInterface マネージド デバッグ アシスタントについて確認します。これは、事前バインディングされた vtable の呼び出しが遅延バインディング専用のクラス インターフェイスで実行されたときに呼び出されます。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), early bound calls AutoDispatch
- dispatch-only mode
- dirtyCastAndCallOnInterface
- early-bound managed classes
- early bound calls on AutoDispatch
- MDAs (managed debugging assistants), early bound calls AutoDispatch
- EarlyBoundCallOnAutorDispatchClassInteface MDA
ms.assetid: aa388ed3-7e3d-48ea-a0b5-c47ae19cec38
ms.openlocfilehash: 49a2930d91e76856436480512360e8b9f9fd3d7a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273582"
---
# <a name="dirtycastandcalloninterface-mda"></a>dirtyCastAndCallOnInterface MDA

`dirtyCastAndCallOnInterface` マネージド デバッグ アシスタント (MDA: Managed Debugging Assistant) は、vtable を使用して事前バインディングされた呼び出しが、遅延バインディング専用とマークされたクラス インターフェイスで試行されたときにアクティブ化されます。  
  
## <a name="symptoms"></a>現象  

 COM 経由で CLR への事前バインディングされた呼び出しが実行されると、アプリケーションはアクセス違反をスローするか、予期しない動作に発生します。  
  
## <a name="cause"></a>原因  

 コードは、遅延バインディング専用のクラス インターフェイス経由で、vtable を使用して事前バインディングされた呼び出しを試行しています。 既定では、クラス インターフェイスは遅延バインディング専用として識別されることに注意してください。 また、<xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性に <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch> 値 (`[ClassInterface(ClassInterfaceType.AutoDispatch)]`) が設定されている場合も、遅延バインディングとして識別されます。  
  
## <a name="resolution"></a>解決方法  

 推奨される解決策としては、COM で使用するための明示的なインターフェイスを定義し、自動生成されるクラス インターフェイスを通してではなく、このインターフェイスを通して、COM クライアント呼び出しを実行するようにする方法があります。 代わりに、`IDispatch` を介して、COM からの呼び出しを遅延バインディングされた呼び出しに変換することもできます。  
  
 事前バインディングされた呼び出しを COM から実行できるように、クラスを <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual> (`[ClassInterface(ClassInterfaceType.AutoDual)]`) として識別することもできます。ただし、「<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>」に記載されているバージョン管理の制約から、<xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual> を使用しないことを強く推奨します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  

 この MDA は CLR に影響しません。 遅延バインディングされたインターフェイス上の事前バインディングされた呼び出しに関するデータを報告するだけです。  
  
## <a name="output"></a>出力  

 事前バインディングでアクセスされたメソッド名またはフィールド名です。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dirtyCastAndCallOnInterface />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
