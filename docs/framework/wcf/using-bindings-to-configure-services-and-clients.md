---
title: サービスとクライアントを構成するためのバインディングの使用
description: バインディングには、WFC クライアントまたはサービスで使用される構成情報が含まれます。 バインディングを定義する方法と、サービス エンドポイントのバインディングを指定する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], using
ms.assetid: c39479c3-0766-4a17-ba4c-97a74607f392
ms.openlocfilehash: 38fa4a928c74f9fff7b67f2479f9304331361fef
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289881"
---
# <a name="using-bindings-to-configure-services-and-clients"></a>サービスとクライアントを構成するためのバインディングの使用

バインディングとは、エンドポイントへの接続に必要な通信の詳細設定を指定するオブジェクトです。 具体的には、バインディングには構成情報が含まれており、この情報を使用してそれぞれのエンドポイントまたはクライアント チャネルで使用されるトランスポート仕様、ワイヤ形式 (メッセージ エンコード) 仕様、プロトコル仕様が定義され、クライアントまたはサービスのランタイムが作成されます。 機能する Windows Communication Foundation (WCF) サービスを作成するには、サービスの各エンドポイントにバインディングが必要です。 ここでは、エンドポイントにおけるバインディングの概要と定義方法、特定のバインディングの指定方法を説明します。  
  
## <a name="what-a-binding-defines"></a>バインディングの定義内容  

 バインディングの情報は、非常に基本的な情報にすることも複雑なものにすることもできます。 最も基本的なバインディングはトランスポート プロトコル (HTTP など) のみを指定したもので、これはエンドポイントへの接続に必ず使用します。 一般的に、バインディングに含まれるエンドポイントへの接続方法を示す情報は、次のカテゴリのいずれかに当てはまります。  
  
 プロトコル  
 使用されているセキュリティ機構 (信頼性の高いメッセージング機能またはトランザクション コンテキストのフロー設定のいずれか) を決定します。  
  
 トランスポート  
 使用する基本のトランスポート プロトコル (TCP や HTTP など) を決定します。  
  
 Encoding  
 メッセージ エンコード (Text/XML、バイナリ、MTOM (Message Transmission Optimization Mechanism) など) を決定します。これは、メッセージをネットワーク上のバイト ストリームとしてどのように表現するかを決定します。  
  
## <a name="system-provided-bindings"></a>システム標準のバインディング  

 WCF に用意されているシステム指定の一連のバインディングは、一般的なアプリケーションの要件とシナリオに対応するように設計されています。 システム指定のバインディングの例のいくつかを次のクラスで示します。  
  
- <xref:System.ServiceModel.BasicHttpBinding> : WS-I Basic Profile 1.1 仕様に準拠する Web サービス (ASP.NET Web サービス (ASMX) ベースのサービスなど) への接続に適した HTTP プロトコル バインディング。  
  
- <xref:System.ServiceModel.WSHttpBinding> : Web サービス仕様のプロトコルに準拠するエンドポイントへの接続に適した HTTP プロトコル バインディング。  
  
- <xref:System.ServiceModel.NetNamedPipeBinding>: .NET バイナリ エンコードとフレーム技術を Windows 名前付きパイプ トランスポートと組み合わせて使用し、同じコンピューター上の他の WCF エンドポイントに接続します。  
  
- <xref:System.ServiceModel.NetMsmqBinding>: .NET バイナリ エンコードとフレーム技術を Message Queuing (MSMQ) と組み合わせて使用し、キューに置かれたメッセージと他の WCF エンドポイントとの接続を作成します。  
  
 システム指定のバインディングの完全な一覧と説明については、「[システム指定のバインド](system-provided-bindings.md)」を参照してください。  
  
## <a name="custom-bindings"></a>カスタム バインディング  

 システム指定のバインディング コレクションに、サービス アプリケーションに必要な機能の適切な組み合わせが含まれていない場合は、<xref:System.ServiceModel.Channels.CustomBinding> バインディングを作成できます。 <xref:System.ServiceModel.Channels.CustomBinding> バインディングの要素の詳細については、「[\<customBinding>](../configure-apps/file-schema/wcf/custombinding.md)」および「[カスタム バインディング](./extending/custom-bindings.md)」を参照してください。  
  
## <a name="using-bindings"></a>バインディングの使用  

 バインディングを使用する際には、次の 2 つの基本手順があります。  
  
1. バインディングを選択、または定義します。 最も簡単な方法は、システム指定のバインディングを 1 つ選択し、それを既定の設定で使用することです。 また、システム指定のバインディングを選択し、そのプロパティを要件に適した値に再設定することもできます。 さらに、カスタム バインドを作成し、すべてのプロパティを必要に応じて設定することもできます。  
  
2. このバインディングを使用するエンドポイントを作成します。  
  
## <a name="code-and-configuration"></a>コードおよび構成  

 バインディングは、コードまたは構成を使用して定義または構成できます。 この 2 つの方法は使用するバインディングの種類に依存しません。たとえば、システム指定のバインディングまたは <xref:System.ServiceModel.Channels.CustomBinding> バインディングのどちらを使用していても関係ありません。 一般に、コードを使用すると、コンパイル時に開発者がバインディングの定義を完全に制御できます。 一方、構成を使用する場合は、システム管理者、または WCF サービスまたはクライアントのユーザーが、バインディングのパラメーターを変更できます。 WCF アプリケーションの展開先の具体的なコンピューター要件やネットワーク条件を予測する方法はないため、この柔軟性が望ましい場合が少なくありません。 バインディング (およびアドレス) 情報がコードから分離されているため、管理者はアプリケーションの再コンパイルや再配置を行わずにバインディングの詳細を変更できます。 バインディングをコードに定義した場合、構成ファイルに記述されている構成ベースの定義はすべて上書きされます。 この方法についての例は、以下のトピックを参照してください。  
  
- [方法: マネージド アプリケーションでの WCF サービスのホスト](how-to-host-a-wcf-service-in-a-managed-application.md)に関する記事では、コード内でバインディングを作成する例が示されています。  
  
- 「[チュートリアル: Windows Communication Foundation クライアントを作成する](how-to-create-a-wcf-client.md)」では、構成を使用してクライアントを作成する例を示しています。  
  
## <a name="see-also"></a>関連項目

- [エンドポイントの作成の概要](endpoint-creation-overview.md)
- [方法: 構成でサービス バインディングを指定する](how-to-specify-a-service-binding-in-configuration.md)
- [方法: コード内でサービス バインディングを指定する](how-to-specify-a-service-binding-in-code.md)
- [方法: 構成でクライアント バインディングを指定する](how-to-specify-a-client-binding-in-configuration.md)
- [方法: コード内でクライアント バインディングを指定する](how-to-specify-a-client-binding-in-code.md)
