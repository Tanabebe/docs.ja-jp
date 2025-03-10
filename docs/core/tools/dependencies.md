---
title: .NET の依存関係を管理する
description: .NET アプリケーションのプロジェクトの依存関係を管理する方法について説明します。
no-loc:
- dotnet add package
- dotnet remove package
- dotnet list package
ms.topic: how-to
ms.date: 01/28/2021
ms.openlocfilehash: 03311902e99962553b5b740a285021f27d94bfbc
ms.sourcegitcommit: 20b4565974d185c7716656a6c63e3cfdbdf4bf41
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2021
ms.locfileid: "104759704"
---
# <a name="manage-dependencies-in-net-applications"></a>.NET アプリケーションの依存関係を管理する

この記事では、プロジェクト ファイルを編集するか、CLI を使用して依存関係を追加および削除する方法について説明します。

## <a name="the-packagereference-element"></a>\<PackageReference> 要素

`<PackageReference>` プロジェクト ファイル要素の構造は次のとおりです。

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" />
```

`Include` 属性では、プロジェクトに追加するパッケージの ID を指定します。 `Version` 属性では、取得するバージョンを指定します。 バージョンは、[NuGet のバージョン ルール](/nuget/create-packages/dependency-versions#version-ranges)に従って指定します。

> [!NOTE]
> プロジェクト ファイルの構文に詳しくない場合は、詳細について、[MSBuild プロジェクトのリファレンス](/visualstudio/msbuild/msbuild-project-file-schema-reference) ドキュメントを参照してください。

次の例に示すように、条件を使用して、特定のターゲットでのみ使用できる依存関係を追加します。

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" Condition="'$(TargetFramework)' == 'netcoreapp2.1'" />
```

前の例の依存関係は、指定されたターゲットでビルドが行われている場合にのみ有効です。 条件の `$(TargetFramework)` は、プロジェクトで設定される MSBuild プロパティです。 最も一般的な .NET アプリケーションの場合、これを行う必要はありません。

## <a name="add-a-dependency-by-editing-the-project-file"></a>プロジェクト ファイルを編集して依存関係を追加する

依存関係を追加するには、`<ItemGroup>` 要素内に `<PackageReference>` 要素を追加します。 既存の `<ItemGroup>` に追加するか、新しく作成することができます。 次の例では、`dotnet new console` によって作成された既定のコンソール アプリケーション プロジェクトを使用しています。

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="3.1.2" />
  </ItemGroup>

</Project>
```

## <a name="add-a-dependency-by-using-the-cli"></a>CLI を使用して依存関係を追加する

依存関係を追加するには、次の例に示すように、[dotnet add package](dotnet-add-package.md) コマンドを実行します。

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore
```

## <a name="remove-a-dependency-by-editing-the-project-file"></a>プロジェクト ファイルを編集して依存関係を削除する

依存関係を削除するには、プロジェクト ファイルから `<PackageReference>` 要素を削除します。

## <a name="remove-a-dependency-by-using-the-cli"></a>CLI を使用して依存関係を削除する

依存関係を削除するには、次の例に示すように、[dotnet remove package](dotnet-remove-package.md) コマンドを実行します。

```dotnetcli
dotnet remove package Microsoft.EntityFrameworkCore
```

## <a name="see-also"></a>関連項目

* [プロジェクト ファイルのパッケージ参照](../project-sdk/msbuild-props.md#reference-properties)
* [dotnet list package コマンド](dotnet-list-package.md)
