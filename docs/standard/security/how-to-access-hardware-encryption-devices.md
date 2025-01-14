---
description: '詳細情報: 方法: ハードウェア暗号化デバイスにアクセスする'
title: '方法: ハードウェア暗号化デバイスにアクセスする'
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- encryption
- key card
- cryptography
- hardware encryption
- CspParameters
ms.assetid: b0e734df-6eb4-4b16-b48c-6f0fe82d5f17
ms.openlocfilehash: fcf12314490542848d20bd3a4977d68c386853bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685271"
---
# <a name="how-to-access-hardware-encryption-devices"></a>方法: ハードウェア暗号化デバイスにアクセスする

> [!NOTE]
> この記事は Windows に適用されます。

ハードウェア暗号化デバイスにアクセスするには、<xref:System.Security.Cryptography.CspParameters> クラスを使用します。 たとえば、このクラスを使用すると、アプリケーションをスマート カード、ハードウェアの乱数ジェネレーター、または特定の暗号化アルゴリズムのハードウェア実装と統合することができます。  

<xref:System.Security.Cryptography.CspParameters> クラスは、正しくインストールされたハードウェア暗号化デバイスにアクセスする暗号化サービス プロバイダー (CSP) を作成します。  レジストリ エディター (Regedit.exe)  を使用してレジストリ キー (HKEY_LOCAL_MACHINE\Software\Microsoft\Cryptography\Defaults\Provider) を調べることで、CSP を使用できるかどうかを確認できます。  
  
### <a name="to-sign-data-using-a-key-card"></a>キー カードを使用してデータに署名するには  
  
1. 整数のプロバイダー型とプロバイダーの名前をコンストラクターに渡す、<xref:System.Security.Cryptography.CspParameters> クラスのインスタンスを新規作成します。  
  
2. 新規作成された <xref:System.Security.Cryptography.CspParameters> オブジェクトの <xref:System.Security.Cryptography.CspParameters.Flags%2A> プロパティに適切なフラグを渡します。  たとえば、<xref:System.Security.Cryptography.CspProviderFlags.UseDefaultKeyContainer> フラグを渡します。  
  
3. <xref:System.Security.Cryptography.CspParameters> オブジェクトをコンストラクターに渡す、<xref:System.Security.Cryptography.AsymmetricAlgorithm> クラス (<xref:System.Security.Cryptography.RSACryptoServiceProvider> クラスなど) のインスタンスを新規作成します。  
  
4. `Sign` メソッドのいずれかを使用してデータに署名し、`Verify` メソッドのいずれかを使用してデータを確認します。  
  
### <a name="to-generate-a-random-number-using-a-hardware-random-number-generator"></a>ハードウェアの乱数ジェネレーターを使用して乱数を生成するには  
  
1. 整数のプロバイダー型とプロバイダーの名前をコンストラクターに渡す、<xref:System.Security.Cryptography.CspParameters> クラスのインスタンスを新規作成します。  
  
2. <xref:System.Security.Cryptography.CspParameters> オブジェクトをコンストラクターに渡す、<xref:System.Security.Cryptography.RNGCryptoServiceProvider> のインスタンスを新規作成します。  
  
3. <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetBytes%2A> メソッドまたは <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetNonZeroBytes%2A> メソッドを使用してランダムな値を作成します。  
  
## <a name="example"></a>例

次のコード例は、スマート カードを使用してデータに署名する方法を示しています。  このコード例は、スマート カードを公開する <xref:System.Security.Cryptography.CspParameters> オブジェクトを作成してから、CSP を使用して <xref:System.Security.Cryptography.RSACryptoServiceProvider> オブジェクトを初期化します。  コード例では、続いて幾らかのデータの署名と確認を行います。  

SHA1 には競合の問題があるため、SHA256 以上をお勧めします。
  
[!code-cpp[Cryptography.SmartCardCSP#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CPP/Cryptography.SmartCardCSP.cpp#1)]
[!code-csharp[Cryptography.SmartCardCSP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CS/example.cs#1)]
[!code-vb[Cryptography.SmartCardCSP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Cryptography.SmartCardCSP/VB/example.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
  
- <xref:System> 名前空間と <xref:System.Security.Cryptography> 名前空間を含めます。  
  
- スマート カード リーダーとドライバーをコンピューターにインストールしておく必要があります。  
  
- カード リーダー固有の情報を使用して、<xref:System.Security.Cryptography.CspParameters> オブジェクトを初期化する必要があります。  詳細については、カード リーダーのドキュメントを参照してください。

## <a name="see-also"></a>関連項目

- [暗号モデル](cryptography-model.md)
- [Cryptographic Services](cryptographic-services.md)
- [クロスプラットフォーム暗号化](cross-platform-cryptography.md)
- [ASP.NET Core データ保護](/aspnet/core/security/data-protection/introduction)
