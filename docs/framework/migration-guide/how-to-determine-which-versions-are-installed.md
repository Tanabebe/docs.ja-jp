---
title: インストールされている .NET Framework バージョンを確認する
description: コード、regedit.exe、または PowerShell を使用して、Windows レジストリに対してクエリを実行することで、コンピューターにインストールされている .NET Framework のバージョンを検出します。
ms.date: 12/04/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining installed versions
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
ms.openlocfilehash: 027c29969b7dd0a2ed0dec62e612754d2d217eed
ms.sourcegitcommit: 1dbe25ff484a02025d5c34146e517c236f7161fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "104653388"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a>方法: インストールされている .NET Framework バージョンを確認する

ユーザーはコンピューターに複数のバージョンの .NET Framework を[インストール](../install/index.md)して実行できます。 アプリを開発または配置する場合、どのバージョンの .NET Framework がユーザーのコンピューターにインストールされているかを確認しなければならない場合があります。 レジストリには、コンピューターにインストールされている .NET Framework のバージョンの一覧が含まれています。

> [!NOTE]
> この記事は .NET Framework に固有のものです。 インストールされている .NET Core および .NET 5 以降の SDK とランタイムを確認するには、「[.NET が既にインストールされていることを確認する方法](../../core/install/how-to-detect-installed-versions.md)」を参照してください。

.NET Framework は、個別にバージョン管理される 2 つの主要コンポーネントで構成されています。

- アプリに機能を提供する型やリソースのコレクションである一連のアセンブリ。 .NET Framework とアセンブリは同じバージョン番号を共有します。 たとえば、.NET Framework のバージョンには、4.5、4.6.1、および 4.7.2 が含まれます。

- アプリのコードを管理および実行する共通言語ランタイム (CLR)。 1 つの CLR バージョンは、通常複数の NET Framework バージョンをサポートしています。 たとえば、CLR バージョン 4.0.30319.*xxxxx* で *xxxxx* が 42000 未満の場合、.NET Framework バージョン 4 から 4.5.2 がサポートされます。 4\.0.30319.42000 以上の CLR バージョンでは、.NET Framework 4.6 以降の .NET Framework バージョンがサポートされます。

コミュニティで管理されているツールを使用して、インストールされている .NET Framework バージョンを検出できます。

- [https://github.com/jmalarcon/DotNetVersions](https://github.com/jmalarcon/DotNetVersions)

  .NET Framework 2.0 のコマンドライン ツール。

- [https://github.com/EliteLoser/DotNetVersionLister](https://github.com/EliteLoser/DotNetVersionLister)

  PowerShell 2.0 モジュール。

.NET Framework の各バージョン用にインストールされている更新プログラムの検出については、「[方法: インストールされている .NET Framework の更新プログラムを確認する](how-to-determine-which-net-framework-updates-are-installed.md)」を参照してください。

## <a name="determine-which-net-implementation-and-version-an-app-is-running-on"></a>アプリが実行されている .NET の実装とバージョンを確認する

<xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> プロパティを使用して、アプリが実行されている .NET の実装とバージョンを照会できます。 アプリが .NET Framework で実行されている場合、出力は次のようになります。

```output
.NET Framework 4.8.4250.0
```

これに対して、アプリが .NET Core または .NET 5 以降で実行されている場合、出力は次のようになります。

```output
.NET Core 3.1.9
.NET 5.0.0
```

## <a name="detect-net-framework-45-and-later-versions"></a>.NET Framework 4.5 以降のバージョンを検出する

コンピューターにインストールされている .NET Framework (4.5 以降) のバージョンは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** のレジストリに一覧されています。 **Full** サブキーが見つからない場合、.NET Framework 4.5 以降はインストールされていません。

> [!NOTE]
> レジストリ パスの **NET Framework Setup** サブキーの先頭は、ピリオドでは "*ありません*"。

レジストリの **Release** REG_DWORD の値は、インストールされている .NET Framework のバージョンを表します。

<a name="version_table"></a>

| .NET Framework のバージョン | **Release** の値 |
| ---------------------- | -------------------------- |
| .NET Framework 4.5     | すべての Windows オペレーティング システム:378389 |
| .NET Framework 4.5.1   | Windows 8.1 および Windows Server 2012 R2:378675<br />他のすべての Windows オペレーティング システム:378758 |
| .NET Framework 4.5.2   | すべての Windows オペレーティング システム:379893 |
| .NET Framework 4.6     | Windows 10:393295<br />他のすべての Windows オペレーティング システム:393297 |
| .NET Framework 4.6.1   | Windows 10 November Update システム:394254<br />他のすべての Windows オペレーティング システム (Windows 10 を含む):394271 |
| .NET Framework 4.6.2   | Windows 10 Anniversary Update および Windows Server 2016 の場合:394802<br />他のすべての Windows オペレーティング システム (他の Windows 10 オペレーティング システムを含む):394806 |
| .NET Framework 4.7     | Windows 10 Creators Update:460798<br />他のすべての Windows オペレーティング システム (他の Windows 10 オペレーティング システムを含む):460805 |
| .NET Framework 4.7.1   | Windows 10 Fall Creators Update および Windows Server バージョン 1709:461308<br/>他のすべての Windows オペレーティング システム (他の Windows 10 オペレーティング システムを含む):461310 |
| .NET Framework 4.7.2   | Windows 10 April 2018 Update および Windows Server バージョン 1803:461808<br/>Windows 10 April 2018 Update および Windows Server バージョン 1803 以外のすべての Windows オペレーティング システム:461814 |
| .NET Framework 4.8     | Windows 10 May 2019 Update および Windows 10 November 2019 Update:528040<br/>On Windows 10 May 2020 Update および Windows 10 October 2020 Update: 528372<br/>他のすべての Windows オペレーティング システム (他の Windows 10 オペレーティング システムを含む):528049 |

### <a name="minimum-version"></a>最小バージョン

.NET Framework の "*最小*" バージョンが存在するかどうかを判断するには、**Release** REG_DWORD 値が次の表にある、それに対応する値以上かどうかを確認します。 たとえば、アプリケーションが .NET Framework 4.8 以降のバージョンで実行されている場合、**Release** REG_DWORD の値が 528040 "*以上*" であることを確認します。

| .NET Framework のバージョン | 最小値 |
| ---------------------- | ------------- |
| .NET Framework 4.5     | 378389 |
| .NET Framework 4.5.1   | 378675 |
| .NET Framework 4.5.2   | 379893 |
| .NET Framework 4.6     | 393295 |
| .NET Framework 4.6.1   | 394254 |
| .NET Framework 4.6.2   | 394802 |
| .NET Framework 4.7     | 460798 |
| .NET Framework 4.7.1   | 461308 |
| .NET Framework 4.7.2   | 461808 |
| .NET Framework 4.8     | 528040 |

### <a name="use-registry-editor"></a>レジストリ エディターを使用する

1. **スタート** メニューの **[ファイル名を指定して実行]** を選択し、「*regedit*」と入力し、 **[OK]** を選択します。

   (regedit を実行するには、管理特権が必要です。)

1. レジストリ エディターで、次のサブキーを開きます。**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**。 **Full** サブキーが存在しない場合は、.NET Framework 4.5 以降はインストールされていません。

1. **Release** という REG_DWORD のエントリを確認します。 それがある場合、.NET Framework 4.5 以降がインストールされています。 その値は、.NET Framework の特定のバージョンに対応しています。 たとえば、次の図では、**Release** エントリの値は 528040 で、これは .NET Framework 4.8 のリリース キーです。

   ![.NET Framework 4.5 のレジストリ エントリ](./media/clr-installdir.png )

### <a name="use-powershell-to-check-for-a-minimum-version"></a>PowerShell を使用して最小バージョンを確認する

PowerShell コマンドを使用し、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** サブキーの **Release** エントリの値を確認します。

次の例では、**Release** エントリの値を確認して、.NET Framework 4.6.2 以降がインストールされているかどうかを判断しています。 このコードでは、インストールされていない場合は、`True` が返され、されている場合は `False` が返されます。

```powershell
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

### <a name="query-the-registry-using-code"></a>コードを使用してレジストリのクエリを実行する

01. <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> メソッドと <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> メソッドを使用し、Windows レジストリの **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** サブキーにアクセスします。

    > [!IMPORTANT]
    > 実行しているアプリが 32 ビットで、64 ビットの Windows で実行されている場合、レジストリ パスは前に示したものとは異なります。 64 ビットのレジストリは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** サブキーで入手できます。 たとえば、.NET Framework 4.5 のレジストリ サブキーは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** になります。

01. **Release** REG_DWORD の値を確認して、インストールされているバージョンを判断します。 上位互換性があるかを確認するには、[.NET Framework のバージョンの表](#version_table)で示されている値以上の値があることを確認します。

次の例では、レジストリから **Release** エントリの値を確認し、インストールされている .NET Framework 4.5 から 4.8 のバージョンを探しています。

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="2":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="2":::

この例では、次のような出力が表示されます。

```output
.NET Framework Version: 4.6.1
```

この例では、バージョンのチェックで推奨されている方法に従います。

- **Release** エントリの値が、既知のリリース キー値 *以上* かどうかを確認しています。
- 最新バージョンから最も古いバージョンの順にチェックします。

## <a name="detect-net-framework-10-through-40"></a>.NET Framework 1.0 から 4.0 を検出する

.NET Framework 1.1 から 4.0 の各バージョンは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP** のサブキーとして一覧されています。 次の表には、各 .NET Framework バージョンへのパスが一覧されています。 ほとんどのバージョンでは、`1` の **Install** REG_DWORD の値があり、このバージョンがインストールされていることを示します。 これらのサブキーには、バージョン文字列を含む **Version** REG_SZ の値もあります。

> [!NOTE]
> レジストリ パスの **NET Framework Setup** サブキーの先頭は、ピリオドでは "*ありません*"。

| Framework のバージョン  | レジストリ サブキー | [値] |
| ------------------ | --------------- | ----- |
| 1.0                | **HKLM\\Software\\Microsoft\\.NETFramework\\Policy\\v1.0\\3705**     | **Install** REG_SZ は `1` と等しい |
| 1.1                | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v1.1.4322**   | **Install** REG_DWORD は `1` と等しい |
| 2.0                | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v2.0.50727**  | **Install** REG_DWORD は `1` と等しい |
| 3.0                | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.0\\Setup** | **InstallSuccess** REG_DWORD は `1` と等しい |
| 3.5                | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.5**        | **Install** REG_DWORD は `1` と等しい |
| 4.0 Client Profile | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Client**  | **Install** REG_DWORD は `1` と等しい |
| 4.0 Full Profile   | **HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**    | **Install** REG_DWORD は `1` と等しい |

> [!IMPORTANT]
> 実行しているアプリが 32 ビットで、64 ビットの Windows で実行されている場合、レジストリ パスは前に示したものとは異なります。 64 ビットのレジストリは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** サブキーで入手できます。 たとえば、.NET Framework 3.5 のレジストリ サブキーは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5** になります。

.NET Framework 1.0 サブキーへのレジストリ パスは、他のものとは異なるので注意してください。

### <a name="use-registry-editor-older-framework-versions"></a>レジストリ エディターを使用する (古いバージョンのフレームワーク)

01. **スタート** メニューの **[ファイル名を指定して実行]** を選択し、「*regedit*」と入力し、 **[OK]** を選択します。

    regedit を実行するには、管理特権が必要です。

01. 確認するバージョンと一致するサブキーを開きます。 「[.NET Framework 1.0 から 4.0 を検出する](#detect-net-framework-10-through-40)」セクションの表を使用します。

    次の図では、.NET Framework 3.5 のサブキーとその **Version** の値を示しています。

    ![.NET Framework 3.5 のレジストリ エントリ。](./media/net-4-and-earlier.png ".NET Framework 3.5 以前のバージョン")

### <a name="query-the-registry-using-code-older-framework-versions"></a>コードを使用してレジストリのクエリを実行する (以前のバージョンのフレームワーク)

<xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> クラスを使用して、Windows レジストリの **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP** サブキーにアクセスします。

> [!IMPORTANT]
> 実行しているアプリが 32 ビットで、64 ビットの Windows で実行されている場合、レジストリ パスは前に示したものとは異なります。 64 ビットのレジストリは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** サブキーで入手できます。 たとえば、.NET Framework 3.5 のレジストリ サブキーは、**HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5** になります。

次の例では、インストールされている .NET Framework のバージョン 1 から 4 が検索されています。

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="1":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="1":::

この例では、以下と類似した出力が表示されます。

```output
v2.0.50727  2.0.50727.4927  SP2
v3.0  3.0.30729.4926  SP2
v3.5  3.5.30729.4926  SP1
v4.0
  Client  4.0.0.0
```

## <a name="find-clr-versions"></a>CLR のバージョンを探す

.NET Framework と共にインストールされる .NET Framework CLR は、個別にバージョン管理されます。 .NET Framework CLR のバージョンを検出するには、2 つの方法があります。

- **Clrver.exe ツール**

  [CLR バージョン ツール (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) を使用して、コンピューターにインストールされている CLR のバージョンを判断します。 [Visual Studio 開発者コマンド プロンプトまたは Visual Studio Developer PowerShell](/visualstudio/ide/reference/command-prompt-powershell) を開いて、`clrver` と入力します。

  出力例

  ```console
  Versions installed on the machine:
  v2.0.50727
  v4.0.30319
  ```

- **`Environment` クラス**

  > [!IMPORTANT]
  > .NET Framework 4.5 以降のバージョンでは、CLR のバージョンの検出に <xref:System.Environment.Version%2A?displayProperty=nameWithType> プロパティを使用しないでください。 代わりに、「[.NET Framework 4.5 以降のバージョンを検出する](#detect-net-framework-45-and-later-versions)」で説明するように、レジストリのクエリを実行します。

  1. <xref:System.Environment.Version?displayProperty=nameWithType> プロパティを照会し、<xref:System.Version> オブジェクトを取得します。

     返された `System.Version` オブジェクトは、現在コードを実行しているランタイムのバージョンを示しています。 コンピューターにインストールされている可能性のある、アセンブリのバージョンやランタイムのその他のバージョンは返されません。

     .NET Framework バージョン 4、4.5、4.5.1、4.5.2 の場合は、返される <xref:System.Version> オブジェクトの文字列表現は 4.0.30319.*xxxxx* という形式です。この *xxxxx* は 42000 未満になります。 .NET Framework 4.6 以降のバージョンの場合は、4.0.30319.42000 という形式です。

  1. **Version** オブジェクトを取得したら、次のようにクエリを実行します。

     - メジャー リリース識別子 (たとえば、バージョン 4.0 の場合の *4*) には、<xref:System.Version.Major%2A?displayProperty=nameWithType> プロパティを使用します。

     - マイナー リリース識別子 (たとえば、バージョン 4.0 の場合の *0*) には、<xref:System.Version.Minor%2A?displayProperty=nameWithType> プロパティを使用します。

     - バージョンの完全な文字列 (たとえば、*4.0.30319.18010*) には、<xref:System.Version.ToString%2A?displayProperty=nameWithType> メソッドを使用します。 このメソッドでは、コードを実行しているランタイムのバージョンを示す値が 1 つ返されます。 コンピューターにインストールされている可能性のあるアセンブリ バージョンやその他のランタイム バージョンは返されません。

  次の例では、<xref:System.Environment.Version%2A?displayProperty=nameWithType> プロパティを使用して CLR バージョンの情報を取得しています。

  ```csharp
  Console.WriteLine($"Version: {Environment.Version}");
  ```

  ```vb
  Console.WriteLine($"Version: {Environment.Version}")
  ```

  この例では、以下と類似した出力が表示されます。

  ```output
  Version: 4.0.30319.18010
  ```

## <a name="see-also"></a>関連項目

- [方法: インストールされている .NET Framework の更新プログラムを確認する](how-to-determine-which-net-framework-updates-are-installed.md)
- [開発者向けの .NET Framework のインストール](../install/guide-for-developers.md)
- [.NET Framework のバージョンおよび依存関係](versions-and-dependencies.md)
