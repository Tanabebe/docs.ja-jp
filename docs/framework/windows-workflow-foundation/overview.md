---
title: Windows Workflow の概要
description: この記事では、実際のプロセスを記述するモデルである Workflow Foundation ワークフローについて説明します。
ms.date: 03/30/2017
ms.assetid: fc44adbe-1412-49ae-81af-0298be44aae6
ms.openlocfilehash: f966aa2b62a743358d4c1ad18f237f988924014d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268678"
---
# <a name="windows-workflow-overview"></a>Windows Workflow の概要

ワークフローは "*アクティビティ*" と呼ばれる要素の集まりであり、これらは実際のプロセスを記述したモデルとして保存されます。 ワークフローでは、短期間だけ行われる業務や長期間にわたって行われる業務の各部分の実行順序と、それらの間の依存関係を表すことができます。 このような業務はモデルの最初から最後まで通して行われます。アクティビティには、人間によって実行されるものと、システム機能によって実行されるものがあります。  
  
## <a name="workflow-run-time-engine"></a>ワークフロー ランタイム エンジン  

 実行されるそれぞれのワークフロー インスタンスは、ホスト プロセスが次のいずれかを通して対話するプロセス内ランタイム エンジンによって作成および保持されます。  
  
- <xref:System.Activities.WorkflowInvoker>。メソッドのようにワークフローを呼び出します。  
  
- <xref:System.Activities.WorkflowApplication>。1 つのワークフロー インスタンスの実行に対して明示的な制御を行います。  
  
- <xref:System.ServiceModel.WorkflowServiceHost>。複数のインスタンスを使用する場合にメッセージ ベースの対話を行います。  
  
 これらの各クラスは、アクティビティの実行に関与する <xref:System.Activities.ActivityInstance> として表されるコアのアクティビティ ランタイムをラップします。 実行するアプリケーション ドメイン内では、同時に複数の <xref:System.Activities.ActivityInstance> オブジェクトを使用できます。  
  
 前述のホストと対話する 3 つのオブジェクトは、それぞれワークフロー プログラムと呼ばれるアクティビティのツリーから作成されます。 ワークフローは、これらの型を使用するか、<xref:System.Activities.ActivityInstance> をラップするカスタムのホストを使用して、コンソール アプリケーション、フォームに基づくアプリケーション、Windows サービス、ASP.NET Web サイト、Windows Communication Foundation (WCF) サービスなどの任意の Windows プロセス内で実行できます。  
  
 ![ホスト プロセス内のワークフローのコンポーネント](./media/44c79d1d-178b-4487-87ed-3e33015a3842.gif "44c79d1d-178b-4487-87ed-3e33015a3842")  
ホスト プロセス内のワークフローのコンポーネント  
  
## <a name="interaction-between-workflow-components"></a>ワークフロー コンポーネント間の対話  

 次の図は、ワークフロー コンポーネントが互いにどのように対話するかを示しています。  
  
 ![ワークフロー コンポーネントがどのように対話するかを示す図。](./media/overview/workflow-component-interatction.gif)  
  
 前の図では、複数のワークフロー インスタンスを呼び出すために、<xref:System.Activities.WorkflowInvoker.Invoke%2A> クラスの <xref:System.Activities.WorkflowInvoker> メソッドが使用されています。 <xref:System.Activities.WorkflowInvoker> は、ホストからの管理が不要の簡易なワークフローに使用されます。ホストからの管理が必要なワークフロー (<xref:System.Activities.Bookmark> の再開など) は、代わりに <xref:System.Activities.WorkflowApplication.Run%2A> を使用して実行する必要があります。 他のワークフロー インスタンスを呼び出す前に、現在のワークフロー インスタンスが完了するのを待機する必要はありません。ランタイム エンジンでは、複数のワークフロー インスタンスの同時実行をサポートしています。  呼び出されるワークフローは次のとおりです。  
  
- <xref:System.Activities.Statements.Sequence> 子アクティビティを含む <xref:System.Activities.Statements.WriteLine> アクティビティ。 親アクティビティの <xref:System.Activities.Variable> は、子アクティビティの <xref:System.Activities.InArgument> にバインドされます。 変数、引数、およびバインドの詳細については、「[変数と引数](variables-and-arguments.md)」を参照してください。  
  
- `ReadLine` という名前のカスタム アクティビティ。 <xref:System.Activities.OutArgument> メソッドの呼び出しに対して `ReadLine` アクティビティの <xref:System.Activities.WorkflowInvoker.Invoke%2A> が返されます。  
  
- <xref:System.Activities.CodeActivity> 抽象クラスから派生するカスタム アクティビティ。 <xref:System.Activities.CodeActivity> は、<xref:System.Activities.CodeActivityContext> メソッドのパラメーターとして使用可能な <xref:System.Activities.CodeActivity.Execute%2A> を使用して、ランタイム機能 (追跡やプロパティなど) にアクセスできます。 これらのランタイム機能の詳細については、「[ワークフロー追跡とトレース](workflow-tracking-and-tracing.md)」と「[ワークフロー実行プロパティ](workflow-execution-properties.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [BizTalk Server 2006 または WF?プロジェクトに最適なワークフロー ツールの選択](/previous-versions/dotnet/articles/cc303238(v=msdn.10))
