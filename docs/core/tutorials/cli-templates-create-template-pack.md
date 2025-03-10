---
title: dotnet new 用のテンプレート パックを作成する
description: dotnet new コマンド用のテンプレート パックをビルドする csproj ファイルを作成する方法を説明します。
author: adegeo
ms.date: 03/26/2021
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 343104f9609c59e7da24f857de6a7fc29803e2df
ms.sourcegitcommit: e7e0921d0a10f85e9cb12f8b87cc1639a6c8d3fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2021
ms.locfileid: "107255390"
---
# <a name="tutorial-create-a-template-pack"></a>チュートリアル: テンプレート パックを作成する

.NET を使用すると、プロジェクト、ファイル、さらにはリソースを生成するテンプレートを作成して配置することができます。 このチュートリアルは、`dotnet new` コマンドで使用するテンプレートの作成、インストール、アンインストール方法を説明するシリーズのパート 3 です。

シリーズのこのパートで学習する内容は次のとおりです。

> [!div class="checklist"]
>
> * テンプレート パックをビルドするための \*.csproj プロジェクトを作成する
> * パックのためのプロジェクト ファイルを構成する
> * NuGet パッケージ ファイルからテンプレートをインストールする
> * パッケージ ID を使用してテンプレートをアンインストールする

## <a name="prerequisites"></a>必須コンポーネント

* このチュートリアル シリーズの[パート 1](cli-templates-create-item-template.md) と[パート 2](cli-templates-create-project-template.md) を完了します。

  このチュートリアルでは、チュートリアルの最初の 2 つのパートで作成した 2 つのテンプレートを使用します。 そのテンプレートをフォルダーとして _working\templates\\_ フォルダー内にコピーしていれば、別のテンプレートを使用することもできます。

* ターミナルを開いて _working\\_ フォルダーに移動します。

## <a name="create-a-template-pack-project"></a>テンプレート パック プロジェクトを作成する

テンプレート パックは、1 つのファイルにパッケージ化された 1 つ以上のテンプレートです。 パックをインストール/アンインストールすると、そのパックに含まれているすべてのテンプレートが追加/削除されます。 このチュートリアル シリーズのこれまでのパートでは、個別のテンプレートのみを扱いました。 パックされていないテンプレートを共有するには、テンプレート フォルダーをコピーし、そのフォルダーを介してインストールする必要があります。 テンプレート パックは複数のテンプレートを含めることができ、1つのファイルであるため、より簡単に共有できます。

テンプレート パックは、NuGet パッケージ ( _.nupkg_) ファイルによって表されます。 また、すべての NuGet パッケージと同様に、テンプレート パックを NuGet フィードにアップロードできます。 `dotnet new -i` コマンドでは、NuGet パッケージ フィードからのテンプレート パックのインストールがサポートされています。 さらに、 _.nupkg_ ファイルからテンプレート パックを直接インストールすることもできます。

通常は、C# プロジェクト ファイルを使用してコードをコンパイルし、バイナリを生成します。 しかし、プロジェクトを使用してテンプレート パックを生成することもできます。 _.csproj_ の設定を変更して、コードがコンパイルされないようにし、代わりにテンプレートのすべての資産をリソースとして含めることができます。 このプロジェクトをビルドすると、テンプレート パックの NuGet パッケージが生成されます。

作成するパックには、これまでに作成した[項目テンプレート](cli-templates-create-item-template.md)と[パッケージ テンプレート](cli-templates-create-project-template.md)が含まれます。 これらの 2 つのテンプレートを _working\templates\\_ フォルダーでグループ化したので、 _.csproj_ ファイル用に _working_ フォルダーを使用できます。

ターミナルで _working_ フォルダーに移動します。 新しいプロジェクトを作成し、名前を `templatepack`、出力フォルダーを現在のフォルダーに設定します。

```dotnetcli
dotnet new console -n templatepack -o .
```

`-n` パラメーターを指定すると、 _.csproj_ のファイル名が _templatepack.csproj_ に設定されます。 `-o` パラメーターを指定すると、現在のディレクトリにファイルが作成されます。 次の出力のような結果が表示されます。

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

次に、お好みのテキスト エディターで _templatepack.csproj_ ファイルを開き、コンテンツを次の XML で置き換えます。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
    <NoWarn>$(NoWarn);NU5128</NoWarn>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

上の XML 内の `<PropertyGroup>` の設定は、3 つのグループに分かれています。 最初のグループでは、NuGet パッケージに必要なプロパティが処理されます。 `<Package*>` の 3 つの設定は、NuGet フィード上でパッケージを識別するための NuGet パッケージ プロパティと関係しています。 具体的には、`<PackageId>` 値は、ディレクトリ パスではなく単一の名前を使用してテンプレート パックをアンインストールするために使用されます。 また、NuGet フィードからテンプレート パックをインストールするためにも使用されます。 `<Title>`、`<PackageTags>` などの残りの設定は、NuGet フィードに表示されるメタデータに関連しています。 NuGet の設定の詳細については、[NuGet と MSBuild のプロパティ](/nuget/reference/msbuild-targets)に関する記事を参照してください。

`<TargetFramework>` の設定は、パック コマンドを実行してプロジェクトのコンパイルとパッケージ化を行うときに MSBuild が正しく実行されるように設定する必要があります。

次の 3 つの設定は、プロジェクトが作成されたときにテンプレートが NuGet パック内の適切なフォルダーに含まれるよう、プロジェクトを正しく構成することに関連しています。

最後の設定を使用すると、テンプレート パック プロジェクトに適用されない警告メッセージを非表示にすることができます。

`<ItemGroup>` には 2 つの設定が含まれています。 まず、`<Content>` 設定では、_templates_ フォルダー内のすべてのものがコンテンツとして含められます。 また、コンパイル済みのコード (テンプレートをテストしてコンパイルした場合) が含まれないようにするために、すべての _bin_ または _obj_ フォルダーを除外するよう設定されます。 次に、`<Compile>` 設定では、すべてのコード ファイルがその場所に関係なくコンパイルから除外されます。 この設定により、テンプレート パックの作成に使用されているプロジェクトで _templates_ フォルダー階層内のコードのコンパイルが試行されなくなります。

## <a name="build-and-install"></a>ビルドしてインストールする

プロジェクト ファイルを保存します。 テンプレート パックを構築する前に、フォルダー構造が正しいことを確認してください。 パックするすべてのテンプレートを、そのフォルダー内の _templates_ フォルダーに配置する必要があります。 フォルダー構造は次のようになります。

```console
working
│   templatepack.csproj
└───templates
    ├───extensions
    │   └───.template.config
    │           template.json
    └───consoleasync
        └───.template.config
                template.json
```

_templates_ フォルダーには、_extensions_ と _consoleasync_ という 2 つのフォルダーがあります。

ターミナルで、_working_ フォルダーから `dotnet pack` コマンドを実行します。 次の出力で示すように、このコマンドによってプロジェクトがビルドされ、_working\bin\Debug_ フォルダーに NuGet パッケージが作成されます。

```console
C:\working> dotnet pack

Microsoft (R) Build Engine version 16.8.0+126527ff1 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

次に、`dotnet new -i PATH_TO_NUPKG_FILE` コマンドを使用してテンプレート パック ファイルをインストールします。

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Example templates: string extensions              stringext                [C#]              Common/Code
Console Application                               console                  [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync             [C#]              Common/Console/C#9
Class library                                     classlib                 [C#], F#, VB      Common/Library
```

NuGet パッケージを NuGet フィードにアップロードした場合は、`dotnet new -i PACKAGEID` コマンドを使用できます。ここで、`PACKAGEID` は _.csproj_ ファイルに含まれる `<PackageId>` 設定と同じです。 このパッケージ ID は、NuGet パッケージ識別子と同じです。

## <a name="uninstall-the-template-pack"></a>テンプレート パックをアンインストールする

テンプレート パックを削除する方法は、テンプレート パックをインストールした方法 (_.nupkg_ ファイルを使用して直接、または NuGet フィードを使用) にかかわらず同じです。 アンインストールするテンプレートの `<PackageId>` を使用します。 `dotnet new -u` コマンドを実行すると、インストールされているテンプレートの一覧を取得できます。

```dotnetcli
C:\working> dotnet new -u

Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ProjectTemplates.2.2
    Details:
      NuGetPackageId: Microsoft.DotNet.Common.ProjectTemplates.2.2
      Version: 1.0.2-beta4
      Author: Microsoft
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
    Uninstall Command:
      dotnet new -u Microsoft.DotNet.Common.ProjectTemplates.2.2

... cut to save space ...

  AdatumCorporation.Utility.Templates
    Details:
      NuGetPackageId: AdatumCorporation.Utility.Templates
      Version: 1.0.0
      Author: Me
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
    Uninstall Command:
      dotnet new -u AdatumCorporation.Utility.Templates
```

`dotnet new -u AdatumCorporation.Utility.Templates` を実行してテンプレートをアンインストールします。 `dotnet new` コマンドを実行するとヘルプ情報が出力され、前にインストールしたテンプレートが除外されているはずです。

おめでとうございます。 テンプレート パックをインストールしてアンインストールしました。

## <a name="next-steps"></a>次のステップ

テンプレートの詳細については、ほとんどを既に説明しましたが、記事「[dotnet new のカスタム テンプレート](../tools/custom-templates.md)」を参照してください。

* [dotnet/templating GitHub リポジトリ Wiki](https://github.com/dotnet/templating/wiki)
* [dotnet/dotnet-template-samples GitHub リポジトリ](https://github.com/dotnet/dotnet-template-samples)
* [JSON Schema Store の *template.json* スキーマ](http://json.schemastore.org/template)
