---
title: .NET SDK 製品利用統計情報
description: 分析に使用する使用状況情報を収集する .NET SDK 製品利用統計情報機能、収集されるデータ、この機能を無効にする方法について説明します。
author: KathleenDollard
ms.date: 08/27/2019
ms.openlocfilehash: cb557973197277b86c5a85770539b3005e7d9e4a
ms.sourcegitcommit: aab60b21144bf04b3057b5d59aa7c58edaef32d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107494221"
---
# <a name="net-sdk-telemetry"></a><span data-ttu-id="5dccd-103">.NET SDK 製品利用統計情報</span><span class="sxs-lookup"><span data-stu-id="5dccd-103">.NET SDK telemetry</span></span>

<span data-ttu-id="5dccd-104">[.NET SDK](index.md) には、.NET CLI がクラッシュしたときに使用状況データと例外情報を収集する製品利用統計情報機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5dccd-104">The [.NET SDK](index.md) includes a telemetry feature that collects usage data and exception information when the .NET CLI crashes.</span></span> <span data-ttu-id="5dccd-105">.NET CLI には .NET SDK が付属しており、.NET アプリをビルド、テスト、公開できるようにする動詞のセットです。</span><span class="sxs-lookup"><span data-stu-id="5dccd-105">The .NET CLI comes with the .NET SDK and is the set of verbs that enable you to build, test, and publish your .NET apps.</span></span> <span data-ttu-id="5dccd-106">.NET Team が、ツールの改善に向けて、その使用方法を把握することが重要です。</span><span class="sxs-lookup"><span data-stu-id="5dccd-106">It's important that the .NET team understands how the tools are used so they can be improved.</span></span> <span data-ttu-id="5dccd-107">エラーに関する情報は、チームが問題を解決し、バグを修正するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-107">Information on failures helps the team resolve problems and fix bugs.</span></span>

<span data-ttu-id="5dccd-108">収集されたデータは、[Creative Commons Attribution License](https://creativecommons.org/licenses/by/4.0/) の下で全体が公開されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-108">The collected data is published in aggregate under the [Creative Commons Attribution License](https://creativecommons.org/licenses/by/4.0/).</span></span>

## <a name="scope"></a><span data-ttu-id="5dccd-109">スコープ</span><span class="sxs-lookup"><span data-stu-id="5dccd-109">Scope</span></span>

<span data-ttu-id="5dccd-110">`dotnet` には、アプリを実行し、CLI コマンドを実行するための 2 つの関数があります。</span><span class="sxs-lookup"><span data-stu-id="5dccd-110">`dotnet` has two functions: to run apps, and to execute CLI commands.</span></span> <span data-ttu-id="5dccd-111">`dotnet` を使用して次の形式でアプリケーションを起動するとき、製品利用統計情報は "*収集されません*"。</span><span class="sxs-lookup"><span data-stu-id="5dccd-111">Telemetry *isn't collected* when using `dotnet` to start an application in the following format:</span></span>

- `dotnet [path-to-app].dll`

<span data-ttu-id="5dccd-112">製品利用統計情報は、次のような [.NET CLI コマンド](index.md)のいずれかを使用するときに "*収集されます*"。</span><span class="sxs-lookup"><span data-stu-id="5dccd-112">Telemetry *is collected* when using any of the [.NET CLI commands](index.md), such as:</span></span>

- `dotnet build`
- `dotnet pack`
- `dotnet run`

## <a name="how-to-opt-out"></a><span data-ttu-id="5dccd-113">オプトアウトする方法</span><span class="sxs-lookup"><span data-stu-id="5dccd-113">How to opt out</span></span>

<span data-ttu-id="5dccd-114">.NET SDK 製品利用統計情報機能は、既定では有効になっています。</span><span class="sxs-lookup"><span data-stu-id="5dccd-114">The .NET SDK telemetry feature is enabled by default.</span></span> <span data-ttu-id="5dccd-115">製品利用統計情報機能をオプトアウトするには、`DOTNET_CLI_TELEMETRY_OPTOUT` 環境変数を `1` または `true` に設定します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-115">To opt out of the telemetry feature, set the `DOTNET_CLI_TELEMETRY_OPTOUT` environment variable to `1` or `true`.</span></span>

<span data-ttu-id="5dccd-116">また、インストールが成功したときにも、.NET SDK インストーラーによって製品利用統計情報の 1 エントリが送信されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-116">A single telemetry entry is also sent by the .NET SDK installer when a successful installation happens.</span></span> <span data-ttu-id="5dccd-117">オプトアウトするには、.NET SDK をインストールする前に `DOTNET_CLI_TELEMETRY_OPTOUT` 環境変数を設定します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-117">To opt out, set the `DOTNET_CLI_TELEMETRY_OPTOUT` environment variable before you install the .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dccd-118">インストーラーの開始後にオプト アウトするには、インストーラーを閉じ、環境変数を設定してから、その値を設定した状態でインストーラーをもう一度実行します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-118">To opt out after you started the installer: close the installer, set the environment variable, and then run the installer again with that value set.</span></span>

## <a name="disclosure"></a><span data-ttu-id="5dccd-119">開示</span><span class="sxs-lookup"><span data-stu-id="5dccd-119">Disclosure</span></span>

<span data-ttu-id="5dccd-120">[.NET CLI コマンド](index.md) (`dotnet build` など) の 1 つを初めて実行すると、.NET SDK により、次のようなテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-120">The .NET SDK displays text similar to the following when you first run one of the [.NET CLI commands](index.md) (for example, `dotnet build`).</span></span> <span data-ttu-id="5dccd-121">テキストは、実行している SDK のバージョンによって多少異なります。</span><span class="sxs-lookup"><span data-stu-id="5dccd-121">Text may vary slightly depending on the version of the SDK you're running.</span></span> <span data-ttu-id="5dccd-122">この "最初の実行" の際に、Microsoft がデータ回収に関して通知する方法が示されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-122">This "first run" experience is how Microsoft notifies you about data collection.</span></span>

```console
Telemetry
---------
The .NET tools collect usage data in order to help us improve your experience. The data is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry
```

<span data-ttu-id="5dccd-123">このメッセージと .NET のウェルカム メッセージを無効にするには、`DOTNET_NOLOGO` 環境変数を `true` に設定します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-123">To disable this message and the .NET welcome message, set the `DOTNET_NOLOGO` environment variable to `true`.</span></span> <span data-ttu-id="5dccd-124">この変数は、テレメトリのオプトアウトには影響しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5dccd-124">Note that this variable has no effect on telemetry opt out.</span></span>

## <a name="data-points"></a><span data-ttu-id="5dccd-125">データ ポイント</span><span class="sxs-lookup"><span data-stu-id="5dccd-125">Data points</span></span>

<span data-ttu-id="5dccd-126">製品利用統計情報機能では、ユーザー名やメール アドレスなどの個人データは収集されません。</span><span class="sxs-lookup"><span data-stu-id="5dccd-126">The telemetry feature doesn't collect personal data, such as usernames or email addresses.</span></span> <span data-ttu-id="5dccd-127">コードはスキャンされず、名前、リポジトリ、作成者などのプロジェクト レベルのデータは抽出されません。</span><span class="sxs-lookup"><span data-stu-id="5dccd-127">It doesn't scan your code and doesn't extract project-level data, such as name, repository, or author.</span></span> <span data-ttu-id="5dccd-128">データは、[Azure Monitor](https://azure.microsoft.com/services/monitor/) テクノロジを使用して Microsoft サーバーに安全に送信され、制限されたアクセスの下で保持され、厳格なセキュリティ コントロールの下で、安全な [Azure Storage](https://azure.microsoft.com/services/storage/) システムから公開されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-128">The data is sent securely to Microsoft servers using [Azure Monitor](https://azure.microsoft.com/services/monitor/) technology, held under restricted access, and published under strict security controls from secure [Azure Storage](https://azure.microsoft.com/services/storage/) systems.</span></span>

<span data-ttu-id="5dccd-129">ユーザーのプライバシー保護は Microsoft にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="5dccd-129">Protecting your privacy is important to us.</span></span> <span data-ttu-id="5dccd-130">製品利用統計情報で機密データが収集されている、またはデータが安全でないか不適切な方法で処理されていることが疑われる場合、[dotnet/sdk](https://github.com/dotnet/sdk/issues) リポジトリで問題を提出するか、[dotnet@microsoft.com](mailto:dotnet@microsoft.com) に電子メールを送信し、調査を依頼してください。</span><span class="sxs-lookup"><span data-stu-id="5dccd-130">If you suspect the telemetry is collecting sensitive data or the data is being insecurely or inappropriately handled, file an issue in the [dotnet/sdk](https://github.com/dotnet/sdk/issues) repository or send an email to [dotnet@microsoft.com](mailto:dotnet@microsoft.com) for investigation.</span></span>

<span data-ttu-id="5dccd-131">製品利用統計情報の機能では次のデータが収集されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-131">The telemetry feature collects the following data:</span></span>

| <span data-ttu-id="5dccd-132">SDK バージョン</span><span class="sxs-lookup"><span data-stu-id="5dccd-132">SDK versions</span></span> | <span data-ttu-id="5dccd-133">データ</span><span class="sxs-lookup"><span data-stu-id="5dccd-133">Data</span></span> |
|--------------|------|
| <span data-ttu-id="5dccd-134">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-134">All</span></span>          | <span data-ttu-id="5dccd-135">呼び出しのタイムスタンプ。</span><span class="sxs-lookup"><span data-stu-id="5dccd-135">Timestamp of invocation.</span></span> |
| <span data-ttu-id="5dccd-136">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-136">All</span></span>          | <span data-ttu-id="5dccd-137">呼び出されたコマンド ("build" など)、2.1 以降はハッシュされます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-137">Command invoked (for example, "build"), hashed starting in 2.1.</span></span> |
| <span data-ttu-id="5dccd-138">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-138">All</span></span>          | <span data-ttu-id="5dccd-139">地理的な場所を決定するために使用する 3 つのオクテットの IP アドレス。</span><span class="sxs-lookup"><span data-stu-id="5dccd-139">Three octet IP address used to determine the geographical location.</span></span> |
| <span data-ttu-id="5dccd-140">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-140">All</span></span>          | <span data-ttu-id="5dccd-141">オペレーティング システムとバージョン。</span><span class="sxs-lookup"><span data-stu-id="5dccd-141">Operating system and version.</span></span> |
| <span data-ttu-id="5dccd-142">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-142">All</span></span>          | <span data-ttu-id="5dccd-143">SDK が実行されているランタイム ID (RID)。</span><span class="sxs-lookup"><span data-stu-id="5dccd-143">Runtime ID (RID) the SDK is running on.</span></span> |
| <span data-ttu-id="5dccd-144">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-144">All</span></span>          | <span data-ttu-id="5dccd-145">.NET SDK のバージョン。</span><span class="sxs-lookup"><span data-stu-id="5dccd-145">.NET SDK version.</span></span> |
| <span data-ttu-id="5dccd-146">すべて</span><span class="sxs-lookup"><span data-stu-id="5dccd-146">All</span></span>          | <span data-ttu-id="5dccd-147">製品利用統計情報プロファイル: 明示的なユーザー オプトインでのみ使用され、Microsoft では内部で使用される任意の値。</span><span class="sxs-lookup"><span data-stu-id="5dccd-147">Telemetry profile: an optional value only used with explicit user opt-in and used internally at Microsoft.</span></span> |
| <span data-ttu-id="5dccd-148">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-148">>=2.0</span></span>        | <span data-ttu-id="5dccd-149">コマンドの引数とオプション: (任意の文字列ではなく) いくつかの引数とオプションが収集されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-149">Command arguments and options: several arguments and options are collected (not arbitrary strings).</span></span> <span data-ttu-id="5dccd-150">[収集されるオプション](#collected-options)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5dccd-150">See [collected options](#collected-options).</span></span> <span data-ttu-id="5dccd-151">2\.1.300 以降はハッシュされます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-151">Hashed after 2.1.300.</span></span> |
| <span data-ttu-id="5dccd-152">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-152">>=2.0</span></span>         | <span data-ttu-id="5dccd-153">SDK がコンテナーで実行されているかどうか。</span><span class="sxs-lookup"><span data-stu-id="5dccd-153">Whether the SDK is running in a container.</span></span> |
| <span data-ttu-id="5dccd-154">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-154">>=2.0</span></span>         | <span data-ttu-id="5dccd-155">ターゲット フレームワーク (`TargetFramework` イベントから)、2.1 以降はハッシュされます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-155">Target frameworks (from the `TargetFramework` event), hashed starting in 2.1.</span></span> |
| <span data-ttu-id="5dccd-156">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-156">>=2.0</span></span>         | <span data-ttu-id="5dccd-157">ハッシュされたメディア アクセス制御 (MAC) アドレス (SHA256)。</span><span class="sxs-lookup"><span data-stu-id="5dccd-157">Hashed Media Access Control (MAC) address (SHA256).</span></span> |
| <span data-ttu-id="5dccd-158">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-158">>=2.0</span></span>         | <span data-ttu-id="5dccd-159">ハッシュされた現在の作業ディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="5dccd-159">Hashed current working directory.</span></span> |
| <span data-ttu-id="5dccd-160">>=2.0</span><span class="sxs-lookup"><span data-stu-id="5dccd-160">>=2.0</span></span>         | <span data-ttu-id="5dccd-161">インストール成功レポート、インストーラーの実行ファイルの名前がハッシュされます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-161">Install success report, with hashed installer exe filename.</span></span> |
| <span data-ttu-id="5dccd-162">>=2.1.300</span><span class="sxs-lookup"><span data-stu-id="5dccd-162">>=2.1.300</span></span>     | <span data-ttu-id="5dccd-163">カーネル バージョン。</span><span class="sxs-lookup"><span data-stu-id="5dccd-163">Kernel version.</span></span> |
| <span data-ttu-id="5dccd-164">>=2.1.300</span><span class="sxs-lookup"><span data-stu-id="5dccd-164">>=2.1.300</span></span>     | <span data-ttu-id="5dccd-165">Libc リリース/バージョン。</span><span class="sxs-lookup"><span data-stu-id="5dccd-165">Libc release/version.</span></span> |
| <span data-ttu-id="5dccd-166">>=3.0.100</span><span class="sxs-lookup"><span data-stu-id="5dccd-166">>=3.0.100</span></span>     | <span data-ttu-id="5dccd-167">出力がリダイレクトされるかどうか (True または False)。</span><span class="sxs-lookup"><span data-stu-id="5dccd-167">Whether the output was redirected (true or false).</span></span> |
| <span data-ttu-id="5dccd-168">>=3.0.100</span><span class="sxs-lookup"><span data-stu-id="5dccd-168">>=3.0.100</span></span>     | <span data-ttu-id="5dccd-169">CLI/SDK クラッシュ時の例外の種類とそのスタック トレース (CLI/SDK コードのみ、送信されたスタック トレースに含まれます)。</span><span class="sxs-lookup"><span data-stu-id="5dccd-169">On a CLI/SDK crash, the exception type and its stack trace (only CLI/SDK code is included in the stack trace sent).</span></span> <span data-ttu-id="5dccd-170">詳細については、「[収集される .NET CLI または SDK クラッシュ例外製品利用統計情報](#net-clisdk-crash-exception-telemetry-collected)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5dccd-170">For more information, see [.NET CLI/SDK crash exception telemetry collected](#net-clisdk-crash-exception-telemetry-collected).</span></span> |
| <span data-ttu-id="5dccd-171">>=5.0.202</span><span class="sxs-lookup"><span data-stu-id="5dccd-171">>=5.0.202</span></span>     | <span data-ttu-id="5dccd-172">プロセスの開始から、CLI プログラムのメイン メソッドに入り、ホストとランタイムの起動を測定するまでの経過時間。</span><span class="sxs-lookup"><span data-stu-id="5dccd-172">Elapsed time from process start until entering the CLI program's main method, measuring host and runtime startup.</span></span> |
| <span data-ttu-id="5dccd-173">>=5.0.202</span><span class="sxs-lookup"><span data-stu-id="5dccd-173">>=5.0.202</span></span>     | <span data-ttu-id="5dccd-174">最初の実行時に .NET ツールをパスに追加するステップの経過時間。</span><span class="sxs-lookup"><span data-stu-id="5dccd-174">Elapsed time for the step that adds .NET Tools to the path on first run.</span></span> |
| <span data-ttu-id="5dccd-175">>=5.0.202</span><span class="sxs-lookup"><span data-stu-id="5dccd-175">>=5.0.202</span></span>     | <span data-ttu-id="5dccd-176">最初の実行時に初回使用通知を表示するための経過時間。</span><span class="sxs-lookup"><span data-stu-id="5dccd-176">Elapsed time to display first time use notice on first run.</span></span> |
| <span data-ttu-id="5dccd-177">>=5.0.202</span><span class="sxs-lookup"><span data-stu-id="5dccd-177">>=5.0.202</span></span>     | <span data-ttu-id="5dccd-178">最初の実行時に ASP.NET 証明書を生成するための経過時間。</span><span class="sxs-lookup"><span data-stu-id="5dccd-178">Elapsed time for generating ASP.NET Certificate on first run.</span></span> |
| <span data-ttu-id="5dccd-179">>=5.0.202</span><span class="sxs-lookup"><span data-stu-id="5dccd-179">>=5.0.202</span></span>     | <span data-ttu-id="5dccd-180">CLI 入力を解析するための経過時間。</span><span class="sxs-lookup"><span data-stu-id="5dccd-180">Elapsed time to parse the CLI input.</span></span> |

### <a name="collected-options"></a><span data-ttu-id="5dccd-181">収集されるオプション</span><span class="sxs-lookup"><span data-stu-id="5dccd-181">Collected options</span></span>

<span data-ttu-id="5dccd-182">一部のコマンドでは、追加データが送信されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-182">Certain commands send additional data.</span></span> <span data-ttu-id="5dccd-183">コマンドのサブセットで最初の引数が送信されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-183">A subset of commands sends the first argument:</span></span>

| <span data-ttu-id="5dccd-184">コマンド</span><span class="sxs-lookup"><span data-stu-id="5dccd-184">Command</span></span>               | <span data-ttu-id="5dccd-185">送信される最初の引数データ</span><span class="sxs-lookup"><span data-stu-id="5dccd-185">First argument data sent</span></span>                |
|-----------------------|-----------------------------------------|
| `dotnet help <arg>`   | <span data-ttu-id="5dccd-186">コマンドのヘルプが求められます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-186">The command help is being queried for.</span></span>  |
| `dotnet new <arg>`    | <span data-ttu-id="5dccd-187">テンプレート名 (ハッシュ済み)。</span><span class="sxs-lookup"><span data-stu-id="5dccd-187">The template name (hashed).</span></span>             |
| `dotnet add <arg>`    | <span data-ttu-id="5dccd-188">`package` または `reference` という単語。</span><span class="sxs-lookup"><span data-stu-id="5dccd-188">The word `package` or `reference`.</span></span>      |
| `dotnet remove <arg>` | <span data-ttu-id="5dccd-189">`package` または `reference` という単語。</span><span class="sxs-lookup"><span data-stu-id="5dccd-189">The word `package` or `reference`.</span></span>      |
| `dotnet list <arg>`   | <span data-ttu-id="5dccd-190">`package` または `reference` という単語。</span><span class="sxs-lookup"><span data-stu-id="5dccd-190">The word `package` or `reference`.</span></span>      |
| `dotnet sln <arg>`    | <span data-ttu-id="5dccd-191">`add`、`list`、または `remove` という単語。</span><span class="sxs-lookup"><span data-stu-id="5dccd-191">The word `add`, `list`, or `remove`.</span></span>    |
| `dotnet nuget <arg>`  | <span data-ttu-id="5dccd-192">`delete`、`locals`、または `push` という単語。</span><span class="sxs-lookup"><span data-stu-id="5dccd-192">The word `delete`, `locals`, or `push`.</span></span> |

<span data-ttu-id="5dccd-193">選択されたオプションが使用される場合は、コマンドのサブセットによって、その値と共に送信されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-193">A subset of commands sends selected options if they're used, along with their values:</span></span>

| <span data-ttu-id="5dccd-194">オプション</span><span class="sxs-lookup"><span data-stu-id="5dccd-194">Option</span></span>                  | <span data-ttu-id="5dccd-195">コマンド</span><span class="sxs-lookup"><span data-stu-id="5dccd-195">Commands</span></span>                                                                                       |
|-------------------------|------------------------------------------------------------------------------------------------|
| `--verbosity`           | <span data-ttu-id="5dccd-196">すべてのコマンド</span><span class="sxs-lookup"><span data-stu-id="5dccd-196">All commands</span></span>                                                                                   |
| `--language`            | `dotnet new`                                                                                   |
| `--configuration`       | <span data-ttu-id="5dccd-197">`dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`</span><span class="sxs-lookup"><span data-stu-id="5dccd-197">`dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`</span></span>                  |
| `--framework`           | <span data-ttu-id="5dccd-198">`dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`, `dotnet vstest`</span><span class="sxs-lookup"><span data-stu-id="5dccd-198">`dotnet build`, `dotnet clean`, `dotnet publish`, `dotnet run`, `dotnet test`, `dotnet vstest`</span></span> |
| `--runtime`             | <span data-ttu-id="5dccd-199">`dotnet build`,  `dotnet publish`</span><span class="sxs-lookup"><span data-stu-id="5dccd-199">`dotnet build`,  `dotnet publish`</span></span>                                                              |
| `--platform`            | `dotnet vstest`                                                                                |
| `--logger`              | `dotnet vstest`                                                                                |
| `--sdk-package-version` | `dotnet migrate`                                                                               |

<span data-ttu-id="5dccd-200">`--verbosity` と `--sdk-package-version` を除き、他のすべての値は .Net Core 2.1.100 SDK 以降、ハッシュされます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-200">Except for `--verbosity` and `--sdk-package-version`, all the other values are hashed starting with .NET Core 2.1.100 SDK.</span></span>

## <a name="net-clisdk-crash-exception-telemetry-collected"></a><span data-ttu-id="5dccd-201">収集される .NET CLI または SDK クラッシュ例外製品利用統計情報</span><span class="sxs-lookup"><span data-stu-id="5dccd-201">.NET CLI/SDK crash exception telemetry collected</span></span>

<span data-ttu-id="5dccd-202">.NET CLI または SDK がクラッシュすると、例外の名前と CLI または SDK コードのスタック トレースが収集されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-202">If the .NET CLI/SDK crashes, it collects the name of the exception and stack trace of the CLI/SDK code.</span></span> <span data-ttu-id="5dccd-203">この情報は、問題を評価し、.NET SDK と CLI の品質を向上させる目的で収集されます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-203">This information is collected to assess problems and improve the quality of the .NET SDK and CLI.</span></span> <span data-ttu-id="5dccd-204">この記事では、Microsoft が収集するデータについて説明します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-204">This article provides information about the data we collect.</span></span> <span data-ttu-id="5dccd-205">また、独自のバージョンの .NET SDK をビルドするユーザーが不注意で個人情報や機密情報を開示してしまわないようにする方法についてのヒントも提供します。</span><span class="sxs-lookup"><span data-stu-id="5dccd-205">It also provides tips on how users building their own version of the .NET SDK can avoid inadvertent disclosure of personal or sensitive information.</span></span>

### <a name="types-of-collected-data"></a><span data-ttu-id="5dccd-206">収集されるデータの種類</span><span class="sxs-lookup"><span data-stu-id="5dccd-206">Types of collected data</span></span>

<span data-ttu-id="5dccd-207">.NET CLI により収集される情報は、CLI および SDK 例外に限定され、アプリケーションの例外は対象外です。</span><span class="sxs-lookup"><span data-stu-id="5dccd-207">.NET CLI collects information for CLI/SDK exceptions only, not exceptions in your application.</span></span> <span data-ttu-id="5dccd-208">収集されたデータには、例外の名前とスタック トレースが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-208">The collected data contains the name of the exception and the stack trace.</span></span> <span data-ttu-id="5dccd-209">このスタック トレースは CLI/SDK コードです。</span><span class="sxs-lookup"><span data-stu-id="5dccd-209">This stack trace is of CLI/SDK code.</span></span>

<span data-ttu-id="5dccd-210">次の例では、収集されたデータの種類を確認できます。</span><span class="sxs-lookup"><span data-stu-id="5dccd-210">The following example shows the kind of data that is collected:</span></span>

```console
System.IO.IOException
at System.ConsolePal.WindowsConsoleStream.Write(Byte[] buffer, Int32 offset, Int32 count)
at System.IO.StreamWriter.Flush(Boolean flushStream, Boolean flushEncoder)
at System.IO.StreamWriter.Write(Char[] buffer)
at System.IO.TextWriter.WriteLine()
at System.IO.TextWriter.SyncTextWriter.WriteLine()
at Microsoft.DotNet.Cli.Utils.Reporter.WriteLine()
at Microsoft.DotNet.Tools.Run.RunCommand.EnsureProjectIsBuilt()
at Microsoft.DotNet.Tools.Run.RunCommand.Execute()
at Microsoft.DotNet.Tools.Run.RunCommand.Run(String[] args)
at Microsoft.DotNet.Cli.Program.ProcessArgs(String[] args, ITelemetry telemetryClient)
at Microsoft.DotNet.Cli.Program.Main(String[] args)
```

### <a name="avoid-inadvertent-disclosure-of-information"></a><span data-ttu-id="5dccd-211">不注意による情報の開示を避ける</span><span class="sxs-lookup"><span data-stu-id="5dccd-211">Avoid inadvertent disclosure of information</span></span>

<span data-ttu-id="5dccd-212">.NET の共同作成者と、自分でビルドした .NET SDK のバージョンを実行しているユーザーは、SDK ソース コードのパスを考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5dccd-212">.NET contributors and anyone else running a version of the .NET SDK that they built themselves should consider the path to their SDK source code.</span></span> <span data-ttu-id="5dccd-213">カスタムのデバッグ ビルドであるか、カスタムのビルド シンボル ファイルで構成されている .NET SDK の使用時にクラッシュが発生した場合、ビルド マシンの SDK ソース ファイル パスがスタック トレースの一部として収集され、ハッシュ化されません。</span><span class="sxs-lookup"><span data-stu-id="5dccd-213">If a crash occurs while using a .NET SDK that is a custom debug build or configured with custom build symbol files, the SDK source file path from the build machine is collected as part of the stack trace and isn't hashed.</span></span>

<span data-ttu-id="5dccd-214">そのため、.NET SDK のカスタム ビルドは、個人情報や機密情報がパス名から明らかになるディレクトリには置かないでください。</span><span class="sxs-lookup"><span data-stu-id="5dccd-214">Because of this, custom builds of the .NET SDK shouldn't be located in directories whose path names expose personal or sensitive information.</span></span>

## <a name="see-also"></a><span data-ttu-id="5dccd-215">関連項目</span><span class="sxs-lookup"><span data-stu-id="5dccd-215">See also</span></span>

- [<span data-ttu-id="5dccd-216">.NET CLI 製品利用統計情報データ</span><span class="sxs-lookup"><span data-stu-id="5dccd-216">.NET CLI Telemetry Data</span></span>](https://dotnet.microsoft.com/platform/telemetry)
- [<span data-ttu-id="5dccd-217">製品利用統計情報の参照のソース (dotnet/sdk リポジトリ)</span><span class="sxs-lookup"><span data-stu-id="5dccd-217">Telemetry reference source (dotnet/sdk repository)</span></span>](https://github.com/dotnet/sdk/tree/main/src/Cli/dotnet/Telemetry)
