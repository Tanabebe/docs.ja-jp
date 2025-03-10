---
title: Windows 互換機能パックを使用してコードを移植する
description: Windows 互換機能パックについて、およびそれを使用して既存の .NET Framework コードを .NET 5 および .NET Core 3.1 に移植する方法について説明します。
author: terrajobst
ms.date: 03/04/2021
ms.openlocfilehash: 655657e38f564d84ea3e56b5374debc04b405eeb
ms.sourcegitcommit: c7f0beaa2bd66ebca86362ca17d673f7e8256ca6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104873641"
---
# <a name="use-the-windows-compatibility-pack-to-port-code-to-net-5"></a>Windows 互換機能パックを使用してコードを .NET 5+ に移植する

既存のコードを .NET Framework から .NET に移植するときに発生する最も一般的な問題の一部として、.NET Framework のみに存在する API およびテクノロジへの依存があります。 "*Windows 互換機能パック*" には、このようなテクノロジの多くが用意されているので、.NET アプリケーションと .NET Standard ライブラリをはるかに簡単に構築できます。

互換性パックは論理的な [.NET Standard 2.0 の拡張機能](../whats-new/dotnet-core-2-0.md#api-changes-and-library-support)であり、API セットが大幅に増加します。 既存のコードは、ほとんど変更されずにコンパイルされます。 "あらゆる .NET 実装で提供される API のセット" でその約束を守るために、レジストリ、Windows Management Instrumentation (WMI)、リフレクション出力 API など、すべてのプラットフォームで動作しないテクノロジは .NET Standard には含まれていません。 Windows 互換機能パックは .NET Standard を基盤とし、これらの Windows 専用のテクノロジにアクセスできるようにします。 .NET に移行したいが、少なくとも最初の手順で Windows に留まることを計画している顧客にとって特に便利です。 このシナリオでは、Windows 専用のテクノロジを使用して、移行の障害を取り除くことができます。

## <a name="package-contents"></a>パッケージの内容

Windows 互換機能パックは、[Microsoft.Windows.Compatibility NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Windows.Compatibility)経由で提供され、.NET または .NET Standard をターゲットとするプロジェクトから参照できます。

Windows 専用 API やプラットフォーム非依存 API など、約 20,000 の API を提供します。テクノロジ領域には次のものがあります。

- コード ページ
- CodeDom
- 構成
- ディレクトリ サービス
- 描画
- ODBC
- アクセス許可
- Port
- Windows アクセス制御リスト (ACL)
- Windows Communication Foundation (WCF)
- Windows 暗号化
- Windows EventLog
- Windows Management Instrumentation (WMI)
- Windows パフォーマンス カウンター
- Windows レジストリ
- Windows ランタイム キャッシュ
- Windows サービス

詳細については、[互換機能パックの仕様](https://github.com/dotnet/designs/blob/main/accepted/2018/compat-pack/compat-pack.md)に関するページを参照してください。

## <a name="get-started"></a>はじめに

1. 移植の前に、[移植プロセス](index.md)を確認してください。

2. .NET または .NET Standard に既存のコードを移植するときに、[Microsoft.Windows.Compatibility NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Windows.Compatibility)をインストールします。

   Windows に留まる場合、すでに用意はできています。

3. .NET アプリケーションまたは .NET Standard ライブラリを Linux または macOS で実行する場合、[API Analyzer](../../standard/analyzers/api-analyzer.md) を使用して、クロスプラットフォームで機能しない API の使用方法を見つけます。

4. そのような API の使用を取り除くか、プラットフォーム非依存の代替で置換するか、プラットフォーム チェックで保護します (以下参照)。

    ```csharp
    private static string GetLoggingPath()
    {
        // Verify the code is running on Windows.
        if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
        {
            using (var key = Registry.CurrentUser.OpenSubKey(@"Software\Fabrikam\AssetManagement"))
            {
                if (key?.GetValue("LoggingDirectoryPath") is string configuredPath)
                    return configuredPath;
            }
        }

        // This is either not running on Windows or no logging path was configured,
        // so just use the path for non-roaming user-specific data files.
        var appDataPath = Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData);
        return Path.Combine(appDataPath, "Fabrikam", "AssetManagement", "Logging");
    }
    ```

デモについては、[Windows 互換機能パックの Channel 9 動画](https://channel9.msdn.com/Events/Connect/2017/T123)をご覧ください。

## <a name="see-also"></a>関連項目

- [.NET Framework から .NET への移植の概要](index.md)
- [ASP.NET から ASP.NET Core への移行](/aspnet/core/migration/proper-to-2x)
- [.NET Framework WPF アプリを .NET に移行する](/dotnet/desktop/wpf/migration/convert-project-from-net-framework?view=netdesktop-5.0&preserve-view=true)
- [.NET Framework Windows フォーム アプリを .NET に移行する](/dotnet/desktop/winforms/migration/?view=netdesktop-5.0&preserve-view=true)
- [.NET Framework ライブラリを .NET に移植する](libraries.md)
