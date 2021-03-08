---
title: アンインストール ツール
description: .NET アンインストール ツールの概要です。これは、.NET SDK とランタイムの制御されたクリーンアップを可能にするガイド付きツールです。
author: sfoslund
ms.date: 01/28/2021
ms.openlocfilehash: 9afcac150659a8f58a04f4c254b0a0219af42e74
ms.sourcegitcommit: 42d436ebc2a7ee02fc1848c7742bc7d80e13fc2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "102105435"
---
# <a name="net-uninstall-tool"></a><span data-ttu-id="b9757-103">.NET アンインストール ツール</span><span class="sxs-lookup"><span data-stu-id="b9757-103">.NET Uninstall Tool</span></span>

<span data-ttu-id="b9757-104">[.NET アンインストール ツール](https://aka.ms/dotnet-core-uninstall-tool) (`dotnet-core-uninstall`) を使用すると、.NET SDK とランタイムをシステムから削除できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-104">The [.NET Uninstall Tool](https://aka.ms/dotnet-core-uninstall-tool) (`dotnet-core-uninstall`) lets you remove .NET SDKs and Runtimes from a system.</span></span> <span data-ttu-id="b9757-105">一連のオプションを使用して、アンインストールするバージョンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-105">A collection of options is available to specify which versions you want to uninstall.</span></span>

<span data-ttu-id="b9757-106">このツールでは、Windows と macOS がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b9757-106">The tool supports Windows and macOS.</span></span> <span data-ttu-id="b9757-107">Linux は現在サポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b9757-107">Linux is currently not supported.</span></span>

<span data-ttu-id="b9757-108">Windows では、ツールは次のいずれかのインストーラーを使用してインストールされた SDK とランタイムのみをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-108">On Windows, the tool can only uninstall SDKs and Runtimes that were installed using one of the following installers:</span></span>

- <span data-ttu-id="b9757-109">.NET SDK およびランタイム インストーラー。</span><span class="sxs-lookup"><span data-stu-id="b9757-109">The .NET SDK and runtime installer.</span></span>
- <span data-ttu-id="b9757-110">Visual Studio 2019 バージョン 16.3 より前のバージョンの Visual Studio インストーラー。</span><span class="sxs-lookup"><span data-stu-id="b9757-110">The Visual Studio installer in versions earlier than Visual Studio 2019 version 16.3.</span></span>

<span data-ttu-id="b9757-111">macOS では、このツールでアンインストールできるのは */usr/local/share/dotnet* フォルダーにある SDK とランタイムのみです。</span><span class="sxs-lookup"><span data-stu-id="b9757-111">On macOS, the tool can only uninstall SDKs and runtimes located in the */usr/local/share/dotnet* folder.</span></span>

<span data-ttu-id="b9757-112">これらの制限のため、このツールでは、コンピューター上の一部の .NET SDK とランタイムをアンインストールできない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-112">Because of these limitations, the tool may not be able to uninstall all of the .NET SDKs and runtimes on your machine.</span></span> <span data-ttu-id="b9757-113">`dotnet --info` コマンドを使用して、インストールされているすべての .NET SDK とランタイム (このツールで削除できない SDK やランタイムを含む) を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="b9757-113">You can use the `dotnet --info` command to find all of the .NET SDKs and runtimes installed, including those SDKs and runtimes that this tool can't remove.</span></span> <span data-ttu-id="b9757-114">`dotnet-core-uninstall list` コマンドを実行すると、このツールでアンインストールできる SDK が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-114">The `dotnet-core-uninstall list` command displays which SDKs can be uninstalled with the tool.</span></span> <span data-ttu-id="b9757-115">バージョン 1.2 以降はバージョン 5.0 以前の SDK とランタイムをアンインストールできます。以前のバージョンのツールは、3.1 以前のものをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-115">Versions 1.2 and later can uninstall SDKs and runtimes with version 5.0 or earlier, and previous versions of the tool can uninstall 3.1 and earlier.</span></span>

## <a name="install-the-tool"></a><span data-ttu-id="b9757-116">ツールをインストールする</span><span class="sxs-lookup"><span data-stu-id="b9757-116">Install the tool</span></span>

<span data-ttu-id="b9757-117">.NET アンインストール ツールは、[ツールのリリース ページ](https://aka.ms/dotnet-core-uninstall-tool)からダウンロードできます。また、ソース コードは [dotnet/cli-lab](https://github.com/dotnet/cli-lab) GitHub リポジトリにあります。</span><span class="sxs-lookup"><span data-stu-id="b9757-117">You can download the .NET Uninstall Tool from [the tool's releases page](https://aka.ms/dotnet-core-uninstall-tool) and find the source code at the [dotnet/cli-lab](https://github.com/dotnet/cli-lab) GitHub repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b9757-118">このツールでは、.NET SDK とランタイムをアンインストールするために昇格が必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-118">The tool requires elevation to uninstall .NET SDKs and runtimes.</span></span> <span data-ttu-id="b9757-119">そのため、Windows では *C:\Program Files*、macOS では */usr/local/bin* などの書き込み保護されたディレクトリにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-119">Therefore, it should be installed in a write-protected directory such as *C:\Program Files* on Windows or */usr/local/bin* on macOS.</span></span> <span data-ttu-id="b9757-120">「[dotnet コマンドの特権アクセス](../tools/elevated-access.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-120">See also [Elevated access for dotnet commands](../tools/elevated-access.md).</span></span> <span data-ttu-id="b9757-121">詳細については、[詳細なインストール手順](https://aka.ms/dotnet-core-uninstall-tool)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-121">For more information, see the [detailed installation instructions](https://aka.ms/dotnet-core-uninstall-tool).</span></span>

## <a name="run-the-tool"></a><span data-ttu-id="b9757-122">ツールを実行します。</span><span class="sxs-lookup"><span data-stu-id="b9757-122">Run the tool</span></span>

<span data-ttu-id="b9757-123">次の手順は、アンインストール ツールを実行するための推奨方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b9757-123">The following steps show the recommended approach for running the uninstall tool:</span></span>

- [<span data-ttu-id="b9757-124">手順 1 - インストールされている .NET SDK とランタイムを表示する</span><span class="sxs-lookup"><span data-stu-id="b9757-124">Step 1 - Display installed .NET SDKs and runtimes</span></span>](#step-1---display-installed-net-sdks-and-runtimes)
- [<span data-ttu-id="b9757-125">手順 2 - ドライ ランを実行する</span><span class="sxs-lookup"><span data-stu-id="b9757-125">Step 2 - Do a dry run</span></span>](#step-2---do-a-dry-run)
- [<span data-ttu-id="b9757-126">手順 3 - .NET SDK とランタイムをアンインストールする</span><span class="sxs-lookup"><span data-stu-id="b9757-126">Step 3 - Uninstall .NET SDKs and Runtimes</span></span>](#step-3---uninstall-net-sdks-and-runtimes)
- [<span data-ttu-id="b9757-127">手順 4 - NuGet フォールバック フォルダーを削除する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="b9757-127">Step 4 - Delete the NuGet fallback folder (optional)</span></span>](#step-4---delete-the-nuget-fallback-folder-optional)

### <a name="step-1---display-installed-net-sdks-and-runtimes"></a><span data-ttu-id="b9757-128">手順 1 - インストールされている .NET SDK とランタイムを表示する</span><span class="sxs-lookup"><span data-stu-id="b9757-128">Step 1 - Display installed .NET SDKs and runtimes</span></span>

<span data-ttu-id="b9757-129">`dotnet-core-uninstall list` コマンドを実行すると、このツールで削除できる、インストールされている .NET SDK とランタイムが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-129">The `dotnet-core-uninstall list` command lists the installed .NET SDKs and runtimes that can be removed with this tool.</span></span> <span data-ttu-id="b9757-130">一部の SDK とランタイムは、Visual Studio で必要な場合があり、それらのアンインストールが推奨されない理由を示す注釈と共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-130">Some SDKs and runtimes may be required by Visual Studio and they're displayed with a note of why it isn't recommended to uninstall them.</span></span>

> [!NOTE]
> <span data-ttu-id="b9757-131">`dotnet-core-uninstall list` コマンドの出力は、ほとんどの場合、`dotnet --info` で出力されるインストールされているバージョンの一覧と一致しません。</span><span class="sxs-lookup"><span data-stu-id="b9757-131">The output of the `dotnet-core-uninstall list` command will not match the list of installed versions in the output of `dotnet --info` in most cases.</span></span> <span data-ttu-id="b9757-132">具体的には、このツールでは、zip ファイルによってインストールされたバージョンや、Visual Studio によって管理されているバージョン (Visual Studio 2019 16.3 以降を使用してインストールされたバージョン) は表示されません。</span><span class="sxs-lookup"><span data-stu-id="b9757-132">Specifically, this tool will not display versions installed by zip files or managed by Visual Studio (any version installed with Visual Studio 2019 16.3 or later).</span></span> <span data-ttu-id="b9757-133">バージョンが Visual Studio によって管理されているかどうかを確認する方法の 1 つは、これを `Add or Remove Programs` で表示することです。そこでは、Visual Studio によって管理されているバージョンの表示名にそれを示すマークが付きます。</span><span class="sxs-lookup"><span data-stu-id="b9757-133">One way to check if a version is managed by Visual Studio is to view it in `Add or Remove Programs`, where Visual Studio managed versions are marked as such in their display names.</span></span>

<span data-ttu-id="b9757-134">**dotnet-core-uninstall list**</span><span class="sxs-lookup"><span data-stu-id="b9757-134">**dotnet-core-uninstall list**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="b9757-135">構文</span><span class="sxs-lookup"><span data-stu-id="b9757-135">Synopsis</span></span>

```console
dotnet-core-uninstall list [options]
```

#### <a name="options"></a><span data-ttu-id="b9757-136">オプション</span><span class="sxs-lookup"><span data-stu-id="b9757-136">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="b9757-137">Windows</span><span class="sxs-lookup"><span data-stu-id="b9757-137">Windows</span></span>](#tab/windows)

* **`--aspnet-runtime`**

  <span data-ttu-id="b9757-138">このツールでアンインストールできるすべての ASP.NET ランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-138">Lists all the ASP.NET Runtimes that can be uninstalled with this tool.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="b9757-139">このツールでアンインストールできるすべての .NET ホスティング バンドルを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-139">Lists all the .NET hosting bundles that can be uninstalled with this tool.</span></span>

* **`--runtime`**

  <span data-ttu-id="b9757-140">このツールでアンインストールできるすべての .NET ランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-140">Lists all .NET Runtimes that can be uninstalled with this tool.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-141">このツールでアンインストールできるすべての .NET SDK を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-141">Lists all .NET SDKs that can be uninstalled with this tool.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-142">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-142">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-143">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-143">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-144">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-144">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="b9757-145">このツールでアンインストールできるすべての x64 .NET SDK とランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-145">Lists all x64 .NET SDKs and runtimes that can be uninstalled with this tool.</span></span>

* **`--x86`**

  <span data-ttu-id="b9757-146">このツールでアンインストールできるすべての x86 .NET SDK とランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-146">Lists all x86 .NET SDKs and runtimes that can be uninstalled with this tool.</span></span>

## <a name="macos"></a>[<span data-ttu-id="b9757-147">macOS</span><span class="sxs-lookup"><span data-stu-id="b9757-147">macOS</span></span>](#tab/macos)

* **`--runtime`**

  <span data-ttu-id="b9757-148">このツールでアンインストールできるすべての .NET ランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-148">Lists all .NET Runtimes that can be uninstalled with this tool.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-149">このツールでアンインストールできるすべての .NET SDK を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-149">Lists all .NET SDKs that can be uninstalled with this tool.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-150">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-150">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-151">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-151">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-152">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-152">The default value is `normal`.</span></span>
  
---

#### <a name="examples"></a><span data-ttu-id="b9757-153">使用例</span><span class="sxs-lookup"><span data-stu-id="b9757-153">Examples</span></span>

* <span data-ttu-id="b9757-154">このツールで削除できるすべての .NET SDK とランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-154">List all .NET SDKs and runtimes that can be removed with this tool:</span></span>

  ```console
  dotnet-core-uninstall list
  ```

* <span data-ttu-id="b9757-155">すべての x64 .NET SDK とランタイムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-155">List all x64 .NET SDKs and runtimes:</span></span>

  ```console
  dotnet-core-uninstall list --x64
  ```

* <span data-ttu-id="b9757-156">すべての x86 .NET SDK を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-156">List all x86 .NET SDKs:</span></span>

  ```console
  dotnet-core-uninstall list --sdk --x86
  ```

### <a name="step-2---do-a-dry-run"></a><span data-ttu-id="b9757-157">手順 2 - ドライ ランを実行する</span><span class="sxs-lookup"><span data-stu-id="b9757-157">Step 2 - Do a dry run</span></span>

<span data-ttu-id="b9757-158">`dotnet-core-uninstall dry-run` および `dotnet-core-uninstall whatif` コマンドでは、アンインストールを実行せずに指定されたオプションに基づいて削除される .NET SDK とランタイムを表示します。</span><span class="sxs-lookup"><span data-stu-id="b9757-158">The `dotnet-core-uninstall dry-run` and `dotnet-core-uninstall whatif` commands display the .NET SDKs and runtimes that will be removed based on the options provided without performing the uninstall.</span></span> <span data-ttu-id="b9757-159">これらのコマンドはシノニムです。</span><span class="sxs-lookup"><span data-stu-id="b9757-159">These commands are synonyms.</span></span>

<span data-ttu-id="b9757-160">**dotnet-core-uninstall dry-run and dotnet-core-uninstall whatif**</span><span class="sxs-lookup"><span data-stu-id="b9757-160">**dotnet-core-uninstall dry-run and dotnet-core-uninstall whatif**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="b9757-161">構文</span><span class="sxs-lookup"><span data-stu-id="b9757-161">Synopsis</span></span>

```console
dotnet-core-uninstall dry-run [options] [<VERSION>...]

dotnet-core-uninstall whatif [options] [<VERSION>...]
```

#### <a name="arguments"></a><span data-ttu-id="b9757-162">引数</span><span class="sxs-lookup"><span data-stu-id="b9757-162">Arguments</span></span>

* **`VERSION`**

  <span data-ttu-id="b9757-163">アンインストールする指定されたバージョン。</span><span class="sxs-lookup"><span data-stu-id="b9757-163">The specified version to uninstall.</span></span> <span data-ttu-id="b9757-164">スペースで区切って、複数のバージョンを順々に指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-164">You may list several versions one after the other, separated by spaces.</span></span> <span data-ttu-id="b9757-165">応答ファイルもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b9757-165">Response files are also supported.</span></span>

  > [!TIP]
  > <span data-ttu-id="b9757-166">すべてのバージョンをコマンド ラインに指定する代わりに応答ファイルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-166">Response files are an alternative to placing all the versions on the command line.</span></span>
  > <span data-ttu-id="b9757-167">それらはテキスト ファイルで、通常、\*.rsp 拡張子が付いています。各バージョンは別々の行に指定されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-167">They're text files, typically with a \*.rsp extension, and each version is listed on a separate line.</span></span>
  > <span data-ttu-id="b9757-168">`VERSION` 引数の応答ファイルを指定するには、\@ 文字を使用し、そのすぐ後に応答ファイル名を指定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-168">To specify a response file for the `VERSION` argument, use the \@ character immediately followed by the response file name.</span></span>

#### <a name="options"></a><span data-ttu-id="b9757-169">オプション</span><span class="sxs-lookup"><span data-stu-id="b9757-169">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="b9757-170">Windows</span><span class="sxs-lookup"><span data-stu-id="b9757-170">Windows</span></span>](#tab/windows)

* **`--all`**

  <span data-ttu-id="b9757-171">すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-171">Removes all .NET SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="b9757-172">指定されたバージョンよりも小さいバージョンの .NET SDK とランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-172">Removes only the .NET SDKs and runtimes with a version smaller than the specified version.</span></span> <span data-ttu-id="b9757-173">指定したバージョンはインストールされたままになります。</span><span class="sxs-lookup"><span data-stu-id="b9757-173">The specified version remains installed.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="b9757-174">指定されたバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-174">Removes all .NET SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="b9757-175">最上位の 1 つのバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-175">Removes .NET SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="b9757-176">上位の修正プログラムによって置き換えられた .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-176">Removes .NET SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="b9757-177">このオプションは、global. json を保護します。</span><span class="sxs-lookup"><span data-stu-id="b9757-177">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="b9757-178">プレビューとしてマークされている .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-178">Removes .NET SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="b9757-179">最上位の 1 つのプレビューを除き、プレビューとしてマークされているすべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-179">Removes .NET SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--aspnet-runtime`**

  <span data-ttu-id="b9757-180">ASP.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-180">Removes ASP.NET Runtimes only.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="b9757-181">.NET ランタイムとホスティングのバンドルのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-181">Removes .NET Runtime and hosting bundles only.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="b9757-182">指定された `major.minor` バージョンに一致する .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-182">Removes .NET SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="b9757-183">.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-183">Removes .NET Runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-184">.NET SDK のみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-184">Removes .NET SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-185">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-185">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-186">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-186">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-187">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-187">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="b9757-188">x64 SDK またはランタイムを削除するには、`--sdk`、`--runtime`、および `--aspnet-runtime` と共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-188">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x64 SDKs or runtimes.</span></span>

* **`--x86`**

  <span data-ttu-id="b9757-189">x86 SDK またはランタイムを削除するには、`--sdk`、`--runtime`、および `--aspnet-runtime` と共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-189">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x86 SDKs or runtimes.</span></span>

* <span data-ttu-id="b9757-190">**`--force`** Visual Studio によって使用される可能性があるバージョンを強制的に削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-190">**`--force`** Forces removal of versions that might be used by Visual Studio.</span></span>

<span data-ttu-id="b9757-191">メモ:</span><span class="sxs-lookup"><span data-stu-id="b9757-191">Notes:</span></span>

1. <span data-ttu-id="b9757-192">`--sdk`、`--runtime`、`--aspnet-runtime`、および `--hosting-bundle` の 1 つだけが必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-192">Exactly one of `--sdk`, `--runtime`, `--aspnet-runtime`, and `--hosting-bundle` is required.</span></span>
2. <span data-ttu-id="b9757-193">`--all`、`--all-below`、`--all-but`、`--all-but-latest`、`--all-lower-patches`、`--all-previews`、`--all-previews-but-latest`、`--major-minor`、および `[<VERSION>...]` は排他的です。</span><span class="sxs-lookup"><span data-stu-id="b9757-193">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>
3. <span data-ttu-id="b9757-194">`--x64` または `--x86` が指定されていない場合は、x64 と x86 の両方が削除されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-194">If `--x64` or `--x86` aren't specified, then both x64 and x86 will be removed.</span></span>

## <a name="macos"></a>[<span data-ttu-id="b9757-195">macOS</span><span class="sxs-lookup"><span data-stu-id="b9757-195">macOS</span></span>](#tab/macos)

* **`--all`**

  <span data-ttu-id="b9757-196">すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-196">Removes all .NET SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="b9757-197">指定されたバージョンより下の .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-197">Removes .NET SDKs and runtimes below the specified version.</span></span> <span data-ttu-id="b9757-198">指定したバージョンはそのまま残ります。</span><span class="sxs-lookup"><span data-stu-id="b9757-198">The specified version will remain.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="b9757-199">指定されたバージョンを除く、.NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-199">Removes .NET SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="b9757-200">最上位の 1 つのバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-200">Removes .NET SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="b9757-201">上位の修正プログラムによって置き換えられた .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-201">Removes .NET SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="b9757-202">このオプションは、global. json を保護します。</span><span class="sxs-lookup"><span data-stu-id="b9757-202">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="b9757-203">プレビューとしてマークされている .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-203">Removes .NET SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="b9757-204">最上位の 1 つのプレビューを除き、プレビューとしてマークされているすべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-204">Removes .NET SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="b9757-205">指定された `major.minor` バージョンに一致する .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-205">Removes .NET SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="b9757-206">.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-206">Removes .NET Runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-207">.NET SDK のみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-207">Removes .NET SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-208">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-208">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-209">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-209">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-210">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-210">The default value is `normal`.</span></span>
  
* <span data-ttu-id="b9757-211">**`--force`** Visual Studio または SDK によって使用される可能性があるバージョンを強制的に削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-211">**`--force`** Forces removal of versions that might be used by Visual Studio or SDKs.</span></span>

<span data-ttu-id="b9757-212">メモ:</span><span class="sxs-lookup"><span data-stu-id="b9757-212">Notes:</span></span>

1. <span data-ttu-id="b9757-213">`--sdk` と `--runtime` のうち 1 つだけが必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-213">Exactly one of `--sdk` and `--runtime` is required.</span></span>
2. <span data-ttu-id="b9757-214">`--all`、`--all-below`、`--all-but`、`--all-but-latest`、`--all-lower-patches`、`--all-previews`、`--all-previews-but-latest`、`--major-minor`、および `[<VERSION>...]` は排他的です。</span><span class="sxs-lookup"><span data-stu-id="b9757-214">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>

---

#### <a name="examples"></a><span data-ttu-id="b9757-215">使用例</span><span class="sxs-lookup"><span data-stu-id="b9757-215">Examples</span></span>

> [!NOTE]
> <span data-ttu-id="b9757-216">既定では、Visual Studio またはその他の SDK に必要な可能性がある .NET SDK とランタイムは `dotnet-core-uninstall dry-run` 出力には含まれません。</span><span class="sxs-lookup"><span data-stu-id="b9757-216">By default, .NET SDKs and runtimes that may be required by Visual Studio or other SDKs are not included in `dotnet-core-uninstall dry-run` output.</span></span> <span data-ttu-id="b9757-217">次の例では、コンピューターの状態によっては、指定された SDK とランタイムの一部が出力に含まれない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-217">In the following examples, some of the specified SDKs and runtimes may not be included in the output, depending on the state of the machine.</span></span> <span data-ttu-id="b9757-218">すべての SDK とランタイムを含めるには、それらを引数として明示的に指定するか、`--force` オプションを使用してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-218">To include all SDKs and runtimes, list them explicitly as arguments or use the `--force` option.</span></span>

* <span data-ttu-id="b9757-219">上位の修正プログラムによって置き換えられたすべての .NET ランタイムを削除するドライ ラン。</span><span class="sxs-lookup"><span data-stu-id="b9757-219">Dry run of removing all .NET Runtimes that have been superseded by higher patches:</span></span>

  ```console
  dotnet-core-uninstall dry-run --all-lower-patches --runtime
  ```

* <span data-ttu-id="b9757-220">バージョン `2.2.301` より下のすべての .NET SDK を削除するドライ ラン。</span><span class="sxs-lookup"><span data-stu-id="b9757-220">Dry run of removing all .NET SDKs below the version `2.2.301`:</span></span>

  ```console
  dotnet-core-uninstall whatif --all-below 2.2.301 --sdk
  ```

### <a name="step-3---uninstall-net-sdks-and-runtimes"></a><span data-ttu-id="b9757-221">手順 3 - .NET SDK とランタイムをアンインストールする</span><span class="sxs-lookup"><span data-stu-id="b9757-221">Step 3 - Uninstall .NET SDKs and Runtimes</span></span>

<span data-ttu-id="b9757-222">`dotnet-core-uninstall remove` では、一連のオプションによって指定された .NET SDK とランタイムをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="b9757-222">`dotnet-core-uninstall remove` uninstalls .NET SDKs and Runtimes that are specified by a collection of options.</span></span> <span data-ttu-id="b9757-223">バージョン 1.2 以降はバージョン 5.0 以前の SDK とランタイムをアンインストールできます。以前のバージョンのツールは、3.1 以前のものをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-223">Versions 1.2 and later can uninstall SDKs and runtimes with version 5.0 or earlier, and previous versions of the tool can uninstall 3.1 and earlier.</span></span>

<span data-ttu-id="b9757-224">このツールには破壊的動作があるため、remove コマンドを実行する前に、ドライ ランを実行することを **強く** お勧めします。</span><span class="sxs-lookup"><span data-stu-id="b9757-224">Since this tool has a destructive behavior, it's **highly** recommended that you do a dry run before running the remove command.</span></span> <span data-ttu-id="b9757-225">ドライ ランにより、`remove` コマンドを使用したときに削除される .NET SDK とランタイムが示されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-225">The dry run will show you what .NET SDKs and runtimes will be removed when you use the `remove` command.</span></span> <span data-ttu-id="b9757-226">削除しても安全な SDK とランタイムを確認するには、「[バージョンを削除する必要はあるか](../install/remove-runtime-sdk-versions.md#should-i-remove-a-version)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-226">Refer to [Should I remove a version?](../install/remove-runtime-sdk-versions.md#should-i-remove-a-version) to learn which SDKs and runtimes are safe to remove.</span></span>

> [!CAUTION]
> <span data-ttu-id="b9757-227">次の注意事項に留意してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-227">Keep in mind the following caveats:</span></span>
>
>- <span data-ttu-id="b9757-228">このツールでは、コンピューター上の `global.json` ファイルに必要な .NET SDK のバージョンをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-228">This tool can uninstall versions of the .NET SDK that are required by `global.json` files on your machine.</span></span> <span data-ttu-id="b9757-229">.NET SDK は、[.NET のダウンロード](https://dotnet.microsoft.com/download/dotnet) ページから再インストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-229">You can reinstall .NET SDKs from the [Download .NET](https://dotnet.microsoft.com/download/dotnet) page.</span></span>
>- <span data-ttu-id="b9757-230">このツールでは、コンピューター上のフレームワークに依存するアプリケーションに必要な .NET ランタイムのバージョンをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-230">This tool can uninstall versions of the .NET Runtime that are required by framework dependent applications on your machine.</span></span> <span data-ttu-id="b9757-231">.NET ランタイムは、[.NET のダウンロード](https://dotnet.microsoft.com/download/dotnet) ページから再インストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-231">You can reinstall .NET Runtimes from the [Download .NET](https://dotnet.microsoft.com/download/dotnet) page.</span></span>
>- <span data-ttu-id="b9757-232">このツールでは、Visual Studio が依存する .NET SDK とランタイムのバージョンをアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-232">This tool can uninstall versions of the .NET SDK and runtime that Visual Studio relies on.</span></span> <span data-ttu-id="b9757-233">Visual Studio のインストールを中断した場合は、Visual Studio インストーラーで [修復] を実行すると稼働状態に戻ります。</span><span class="sxs-lookup"><span data-stu-id="b9757-233">If you break your Visual Studio installation, run "Repair" in the Visual Studio installer to get back to a working state.</span></span>

<span data-ttu-id="b9757-234">既定で、すべてのコマンドでは、Visual Studio またはその他の SDK に必要な可能性がある .NET SDK とランタイムを保持します。</span><span class="sxs-lookup"><span data-stu-id="b9757-234">By default, all commands keep the .NET SDKs and runtimes that may be required by Visual Studio or other SDKs.</span></span> <span data-ttu-id="b9757-235">これらの SDK とランタイムは、引数として明示的に指定するか、`--force` オプションを使用することによってアンインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-235">These SDKs and runtimes can be uninstalled by listing them explicitly as arguments or by using the `--force` option.</span></span>

<span data-ttu-id="b9757-236">このツールでは、.NET SDK とランタイムをアンインストールするために昇格が必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-236">The tool requires elevation to uninstall .NET SDKs and runtimes.</span></span> <span data-ttu-id="b9757-237">Windows では管理者コマンド プロンプトで、macOS では `sudo` を使用してツールを実行してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-237">Run the tool in an Administrator command prompt on Windows and with `sudo` on macOS.</span></span> <span data-ttu-id="b9757-238">`dry-run` および `whatif` コマンドには、昇格は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b9757-238">The `dry-run` and `whatif` commands don't require elevation.</span></span>

<span data-ttu-id="b9757-239">**dotnet-core-uninstall remove**</span><span class="sxs-lookup"><span data-stu-id="b9757-239">**dotnet-core-uninstall remove**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="b9757-240">構文</span><span class="sxs-lookup"><span data-stu-id="b9757-240">Synopsis</span></span>

```console
dotnet-core-uninstall remove [options] [<VERSION>...]
```

#### <a name="arguments"></a><span data-ttu-id="b9757-241">引数</span><span class="sxs-lookup"><span data-stu-id="b9757-241">Arguments</span></span>

* **`VERSION`**

  <span data-ttu-id="b9757-242">アンインストールする指定されたバージョン。</span><span class="sxs-lookup"><span data-stu-id="b9757-242">The specified version to uninstall.</span></span> <span data-ttu-id="b9757-243">スペースで区切って、複数のバージョンを順々に指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-243">You may list several versions one after the other, separated by spaces.</span></span> <span data-ttu-id="b9757-244">応答ファイルもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b9757-244">Response files are also supported.</span></span>

  > [!TIP]
  > <span data-ttu-id="b9757-245">すべてのバージョンをコマンド ラインに指定する代わりに応答ファイルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b9757-245">Response files are an alternative to placing all the versions on the command line.</span></span>
  > <span data-ttu-id="b9757-246">それらはテキスト ファイルで、通常、\*.rsp 拡張子が付いています。各バージョンは別々の行に指定されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-246">They're text files, typically with a \*.rsp extension, and each version is listed on a separate line.</span></span>
  > <span data-ttu-id="b9757-247">`VERSION` 引数の応答ファイルを指定するには、\@ 文字を使用し、そのすぐ後に応答ファイル名を指定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-247">To specify a response file for the `VERSION` argument, use the \@ character immediately followed by the response file name.</span></span>

#### <a name="options"></a><span data-ttu-id="b9757-248">オプション</span><span class="sxs-lookup"><span data-stu-id="b9757-248">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="b9757-249">Windows</span><span class="sxs-lookup"><span data-stu-id="b9757-249">Windows</span></span>](#tab/windows)

* **`--all`**

  <span data-ttu-id="b9757-250">すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-250">Removes all .NET SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="b9757-251">指定されたバージョンよりも小さいバージョンの .NET SDK とランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-251">Removes only the .NET SDKs and runtimes with a version smaller than the specified version.</span></span> <span data-ttu-id="b9757-252">指定したバージョンはインストールされたままになります。</span><span class="sxs-lookup"><span data-stu-id="b9757-252">The specified version remains installed.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="b9757-253">指定されたバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-253">Removes all .NET SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="b9757-254">最上位の 1 つのバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-254">Removes .NET SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="b9757-255">上位の修正プログラムによって置き換えられた .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-255">Removes .NET SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="b9757-256">このオプションは、global. json を保護します。</span><span class="sxs-lookup"><span data-stu-id="b9757-256">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="b9757-257">プレビューとしてマークされている .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-257">Removes .NET SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="b9757-258">最上位の 1 つのプレビューを除き、プレビューとしてマークされているすべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-258">Removes .NET SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--aspnet-runtime`**

  <span data-ttu-id="b9757-259">ASP.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-259">Removes ASP.NET Runtimes only.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="b9757-260">.NET ホスティングのバンドルのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-260">Removes .NET hosting bundles only.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="b9757-261">指定された `major.minor` バージョンに一致する .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-261">Removes .NET SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="b9757-262">.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-262">Removes .NET Runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-263">.NET SDK のみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-263">Removes .NET SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-264">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-264">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-265">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-265">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-266">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-266">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="b9757-267">x64 SDK またはランタイムを削除するには、`--sdk`、`--runtime`、および `--aspnet-runtime` と共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-267">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x64 SDKs or runtimes.</span></span>

* **`--x86`**

  <span data-ttu-id="b9757-268">x86 SDK またはランタイムを削除するには、`--sdk`、`--runtime`、および `--aspnet-runtime` と共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-268">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x86 SDKs or runtimes.</span></span>

* <span data-ttu-id="b9757-269">**`-y, --yes`** Yes または No の確認を要求せずにコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="b9757-269">**`-y, --yes`** Executes the command without requiring a yes or no confirmation.</span></span>

* <span data-ttu-id="b9757-270">**`--force`** Visual Studio によって使用される可能性があるバージョンを強制的に削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-270">**`--force`** Forces removal of versions that might be used by Visual Studio.</span></span>

<span data-ttu-id="b9757-271">メモ:</span><span class="sxs-lookup"><span data-stu-id="b9757-271">Notes:</span></span>

1. <span data-ttu-id="b9757-272">`--sdk`、`--runtime`、`--aspnet-runtime`、および `--hosting-bundle` の 1 つだけが必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-272">Exactly one of `--sdk`, `--runtime`, `--aspnet-runtime`, and `--hosting-bundle` is required.</span></span>
2. <span data-ttu-id="b9757-273">`--all`、`--all-below`、`--all-but`、`--all-but-latest`、`--all-lower-patches`、`--all-previews`、`--all-previews-but-latest`、`--major-minor`、および `[<VERSION>...]` は排他的です。</span><span class="sxs-lookup"><span data-stu-id="b9757-273">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>
3. <span data-ttu-id="b9757-274">`--x64` または `--x86` が指定されていない場合は、x64 と x86 の両方が削除されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-274">If `--x64` or `--x86` aren't specified, then both x64 and x86 will be removed.</span></span>

## <a name="macos"></a>[<span data-ttu-id="b9757-275">macOS</span><span class="sxs-lookup"><span data-stu-id="b9757-275">macOS</span></span>](#tab/macos)

* **`--all`**

  <span data-ttu-id="b9757-276">すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-276">Removes all .NET SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="b9757-277">指定されたバージョンより下の .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-277">Removes .NET SDKs and runtimes below the specified version.</span></span> <span data-ttu-id="b9757-278">指定したバージョンはそのまま残ります。</span><span class="sxs-lookup"><span data-stu-id="b9757-278">The specified version will remain.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="b9757-279">指定されたバージョンを除く、.NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-279">Removes .NET SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="b9757-280">最上位の 1 つのバージョンを除く、すべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-280">Removes .NET SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="b9757-281">上位の修正プログラムによって置き換えられた .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-281">Removes .NET SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="b9757-282">このオプションは、global. json を保護します。</span><span class="sxs-lookup"><span data-stu-id="b9757-282">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="b9757-283">プレビューとしてマークされている .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-283">Removes .NET SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="b9757-284">最上位の 1 つのプレビューを除き、プレビューとしてマークされているすべての .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-284">Removes .NET SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="b9757-285">指定された `major.minor` バージョンに一致する .NET SDK とランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-285">Removes .NET SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="b9757-286">.NET ランタイムのみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-286">Removes .NET Runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="b9757-287">.NET SDK のみを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-287">Removes .NET SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="b9757-288">詳細レベルを設定します。</span><span class="sxs-lookup"><span data-stu-id="b9757-288">Sets the verbosity level.</span></span> <span data-ttu-id="b9757-289">指定できる値は、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-289">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="b9757-290">既定値は `normal` です。</span><span class="sxs-lookup"><span data-stu-id="b9757-290">The default value is `normal`.</span></span>

* <span data-ttu-id="b9757-291">**`-y, --yes`** Y/N の確認を要求せずにコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="b9757-291">**`-y, --yes`** Executes the command without requiring Y/N confirmation.</span></span>
  
* <span data-ttu-id="b9757-292">**`--force`** Visual Studio または SDK によって使用される可能性があるバージョンを強制的に削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-292">**`--force`** Forces removal of versions that might be used by Visual Studio or SDKs.</span></span>

<span data-ttu-id="b9757-293">メモ:</span><span class="sxs-lookup"><span data-stu-id="b9757-293">Notes:</span></span>

1. <span data-ttu-id="b9757-294">`--sdk` と `--runtime` のうち 1 つだけが必要です。</span><span class="sxs-lookup"><span data-stu-id="b9757-294">Exactly one of `--sdk` and `--runtime` is required.</span></span>
2. <span data-ttu-id="b9757-295">`--all`、`--all-below`、`--all-but`、`--all-but-latest`、`--all-lower-patches`、`--all-previews`、`--all-previews-but-latest`、`--major-minor`、および `[<VERSION>...]` は排他的です。</span><span class="sxs-lookup"><span data-stu-id="b9757-295">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>

---

#### <a name="examples"></a><span data-ttu-id="b9757-296">使用例</span><span class="sxs-lookup"><span data-stu-id="b9757-296">Examples</span></span>

> [!NOTE]
> <span data-ttu-id="b9757-297">既定で、Visual Studio またはその他の SDK に必要な可能性がある .NET SDK とランタイムは保持されます。</span><span class="sxs-lookup"><span data-stu-id="b9757-297">By default, .NET SDKs and runtimes that may be required by Visual Studio or other SDKs are kept.</span></span> <span data-ttu-id="b9757-298">次の例では、コンピューターの状態によっては、指定された SDK とランタイムの一部が保持される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b9757-298">In the following examples, some of the specified SDKs and runtimes may remain, depending on the state of the machine.</span></span> <span data-ttu-id="b9757-299">すべての SDK とランタイムを削除するには、それらを引数として明示的に指定するか、`--force` オプションを使用してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-299">To remove all SDKs and runtimes, list them explicitly as arguments or use the `--force` option.</span></span>

* <span data-ttu-id="b9757-300">Y/N の確認を要求せずに、バージョン `3.0.0-preview6-27804-01` を除くすべての .NET ランタイムを削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-300">Remove all .NET Runtimes except the version `3.0.0-preview6-27804-01` without requiring Y/N confirmation:</span></span>

  ```console
  dotnet-core-uninstall remove --all-but 3.0.0-preview6-27804-01 --runtime --yes
  ```

* <span data-ttu-id="b9757-301">Y/N の確認を要求せずに、すべての .NET Core 1.1 SDK を削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-301">Remove all .NET Core 1.1 SDKs without requiring Y/n confirmation:</span></span>

  ```console
  dotnet-core-uninstall remove --sdk --major-minor 1.1 -y
  ```

* <span data-ttu-id="b9757-302">コンソールに出力せずに、.NET Core 1.1.11 SDK を削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-302">Remove the .NET Core 1.1.11 SDK with no console output:</span></span>

  ```console
  dotnet-core-uninstall remove 1.1.11 --sdk --yes --verbosity q
  ```

* <span data-ttu-id="b9757-303">このツールで安全に削除できるすべての .NET SDK を削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-303">Remove all .NET SDKs that can safely be removed by this tool:</span></span>

  ```console
  dotnet-core-uninstall remove --all --sdk
  ```

* <span data-ttu-id="b9757-304">Visual Studio で必要な可能性がある SDK を含め、このツールで削除できるすべての .NET SDK を削除します (推奨されません)。</span><span class="sxs-lookup"><span data-stu-id="b9757-304">Remove all .NET SDKs that can be removed by this tool, including those SDKs that may be required by Visual Studio (not recommended):</span></span>

  ```console
  dotnet-core-uninstall remove --all --sdk --force
  ```

* <span data-ttu-id="b9757-305">応答ファイル `versions.rsp` に指定されたすべての .NET SDK を削除します</span><span class="sxs-lookup"><span data-stu-id="b9757-305">Remove all .NET SDKs that are specified in the response file `versions.rsp`</span></span>

  ```console
  dotnet-core-uninstall remove --sdk @versions.rsp
  ```

  <span data-ttu-id="b9757-306">*versions.rsp* の内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b9757-306">The content of *versions.rsp* is as follows:</span></span>
  
  ```text
  2.2.300
  2.1.700
  ```

### <a name="step-4---delete-the-nuget-fallback-folder-optional"></a><span data-ttu-id="b9757-307">手順 4 - NuGet フォールバック フォルダーを削除する (省略可能)</span><span class="sxs-lookup"><span data-stu-id="b9757-307">Step 4 - Delete the NuGet fallback folder (optional)</span></span>

<span data-ttu-id="b9757-308">場合によっては、`NuGetFallbackFolder` が不要になり、削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="b9757-308">In some cases, you no longer need the `NuGetFallbackFolder` and may wish to delete it.</span></span> <span data-ttu-id="b9757-309">このフォルダーの削除の詳細については、[NuGetFallbackFolder の削除](../install/remove-runtime-sdk-versions.md#remove-the-nuget-fallback-folder)に関する記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-309">For more information about deleting this folder, see [Remove the NuGetFallbackFolder](../install/remove-runtime-sdk-versions.md#remove-the-nuget-fallback-folder).</span></span>

## <a name="uninstall-the-tool"></a><span data-ttu-id="b9757-310">ツールをアンインストールする</span><span class="sxs-lookup"><span data-stu-id="b9757-310">Uninstall the tool</span></span>

## <a name="windows"></a>[<span data-ttu-id="b9757-311">Windows</span><span class="sxs-lookup"><span data-stu-id="b9757-311">Windows</span></span>](#tab/windows)

1. <span data-ttu-id="b9757-312">**[プログラムの追加と削除]** を開きます。</span><span class="sxs-lookup"><span data-stu-id="b9757-312">Open **Add or Remove Programs**.</span></span>
2. <span data-ttu-id="b9757-313">`Microsoft .NET SDK Uninstall Tool` を検索します。</span><span class="sxs-lookup"><span data-stu-id="b9757-313">Search for `Microsoft .NET SDK Uninstall Tool`.</span></span>
3. <span data-ttu-id="b9757-314">**[アンインストール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b9757-314">Select **Uninstall**.</span></span>

## <a name="macos"></a>[<span data-ttu-id="b9757-315">macOS</span><span class="sxs-lookup"><span data-stu-id="b9757-315">macOS</span></span>](#tab/macos)

<span data-ttu-id="b9757-316">ダウンロードした *dotnet-core-uninstall.tar.gz* ファイルをインストールしたディレクトリから削除します。</span><span class="sxs-lookup"><span data-stu-id="b9757-316">Delete the downloaded *dotnet-core-uninstall.tar.gz* file from the directory where it was installed.</span></span> <span data-ttu-id="b9757-317">このファイルの内容を別のディレクトリに解凍した場合は、必ずその内容も削除してください。</span><span class="sxs-lookup"><span data-stu-id="b9757-317">If you unzipped the contents of this file into another directory, be sure to delete that content as well.</span></span>

---
