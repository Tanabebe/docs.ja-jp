---
ms.openlocfilehash: 94d2f0acd34532c9c9960fee87b6ef657f04cd72
ms.sourcegitcommit: aab60b21144bf04b3057b5d59aa7c58edaef32d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107494319"
---
### <a name="path-apis-dont-throw-an-exception-for-invalid-characters"></a><span data-ttu-id="c3e41-101">パス API から、無効な文字に対する例外はスローされません</span><span class="sxs-lookup"><span data-stu-id="c3e41-101">Path APIs don't throw an exception for invalid characters</span></span>

<span data-ttu-id="c3e41-102">ファイル パスを必要とする API では、パス文字の検証も、無効な文字が見つかった場合の \`M:System.ArgumentException> のスローも行わなくなりました。</span><span class="sxs-lookup"><span data-stu-id="c3e41-102">APIs that involve file paths no longer validate path characters or throw an \`M:System.ArgumentException> if an invalid character is found.</span></span>

#### <a name="change-description"></a><span data-ttu-id="c3e41-103">変更の説明</span><span class="sxs-lookup"><span data-stu-id="c3e41-103">Change description</span></span>

<span data-ttu-id="c3e41-104">.NET Framework と .NET Core 1.0 - 2.0 では、パス引数に無効なパス文字が含まれている場合、[影響を受ける API](#affected-apis) セクションにリストされているメソッドからは、<xref:System.ArgumentException> がスローされます。</span><span class="sxs-lookup"><span data-stu-id="c3e41-104">In .NET Framework and .NET Core 1.0 - 2.0, the methods listed in the [Affected APIs](#affected-apis) section throw an <xref:System.ArgumentException> if the path argument contains an invalid path character.</span></span> <span data-ttu-id="c3e41-105">.NET Core 2.1 以降、これらのメソッドでは、[無効なパス文字](xref:System.IO.Path.GetInvalidPathChars%2A)をチェックすることも、無効な文字が見つかった場合に例外をスローすることも行われなくなりました。</span><span class="sxs-lookup"><span data-stu-id="c3e41-105">Starting in .NET Core 2.1, these methods no longer check for [invalid path characters](xref:System.IO.Path.GetInvalidPathChars%2A) or throw an exception if an invalid character is found.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="c3e41-106">変更理由</span><span class="sxs-lookup"><span data-stu-id="c3e41-106">Reason for change</span></span>

<span data-ttu-id="c3e41-107">パス文字を積極的に検証すると、一部のクロスプラットフォーム シナリオがブロックされます。</span><span class="sxs-lookup"><span data-stu-id="c3e41-107">Aggressive validation of path characters blocks some cross-platform scenarios.</span></span> <span data-ttu-id="c3e41-108">この変更は、オペレーティング システムの API 呼び出しの結果をレプリケートまたは予測する試みが .NET によって行われないようにするために導入されました。</span><span class="sxs-lookup"><span data-stu-id="c3e41-108">This change was introduced so that .NET does not try to replicate or predict the outcome of operating system API calls.</span></span> <span data-ttu-id="c3e41-109">詳細については、ブログ記事「[.NET Core 2.1 の System.IO の先行プレビュー](/archive/blogs/jeremykuhne/system-io-in-net-core-2-1-sneak-peek)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c3e41-109">For more information, see the [System.IO in .NET Core 2.1 sneak peek](/archive/blogs/jeremykuhne/system-io-in-net-core-2-1-sneak-peek) blog post.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="c3e41-110">導入されたバージョン</span><span class="sxs-lookup"><span data-stu-id="c3e41-110">Version introduced</span></span>

<span data-ttu-id="c3e41-111">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="c3e41-111">.NET Core 2.1</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="c3e41-112">推奨される操作</span><span class="sxs-lookup"><span data-stu-id="c3e41-112">Recommended action</span></span>

<span data-ttu-id="c3e41-113">ご利用のコードが無効な文字のチェックする上で、これらの API に依存していた場合は、<xref:System.IO.Path.GetInvalidPathChars%2A?displayProperty=nameWithType> の呼び出しを追加できます。</span><span class="sxs-lookup"><span data-stu-id="c3e41-113">If your code relied on these APIs to check for invalid characters, you can add a call to <xref:System.IO.Path.GetInvalidPathChars%2A?displayProperty=nameWithType>.</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="c3e41-114">影響を受ける API</span><span class="sxs-lookup"><span data-stu-id="c3e41-114">Affected APIs</span></span>

- <xref:System.IO.Directory.CreateDirectory%2A?displayProperty=fullName>
- <xref:System.IO.Directory.Delete%2A?displayProperty=fullName>
- <xref:System.IO.Directory.EnumerateDirectories%2A?displayProperty=fullName>
- <xref:System.IO.Directory.EnumerateFiles%2A?displayProperty=fullName>
- <xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=fullName>
- <xref:System.IO.Directory.GetCreationTime(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetCreationTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetDirectories%2A?displayProperty=fullName>
- <xref:System.IO.Directory.GetDirectoryRoot(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetFiles%2A?displayProperty=fullName>
- <xref:System.IO.Directory.GetFileSystemEntries%2A?displayProperty=fullName>
- <xref:System.IO.Directory.GetLastAccessTime(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetLastAccessTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetLastWriteTime(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetLastWriteTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.GetParent(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.Move(System.String,System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.SetCreationTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.Directory.SetCreationTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.Directory.SetCurrentDirectory(System.String)?displayProperty=fullName>
- <xref:System.IO.Directory.SetLastAccessTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.Directory.SetLastAccessTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.Directory.SetLastWriteTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.Directory.SetLastWriteTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <span data-ttu-id="c3e41-115">[System.IO.DirectoryInfo ctor](xref:System.IO.DirectoryInfo.%23ctor(System.String))</span><span class="sxs-lookup"><span data-stu-id="c3e41-115">[System.IO.DirectoryInfo ctor](xref:System.IO.DirectoryInfo.%23ctor(System.String))</span></span>
- <xref:System.IO.Directory.GetDirectories%2A?displayProperty=fullName>
- <xref:System.IO.Directory.GetFiles%2A?displayProperty=fullName>
- <xref:System.IO.DirectoryInfo.GetFileSystemInfos%2A?displayProperty=fullName>
- <xref:System.IO.File.AppendAllText%2A?displayProperty=fullName>
- <xref:System.IO.File.AppendAllTextAsync%2A?displayProperty=fullName>
- <xref:System.IO.File.Copy%2A?displayProperty=fullName>
- <xref:System.IO.File.Create%2A?displayProperty=fullName>
- <xref:System.IO.File.CreateText%2A?displayProperty=fullName>
- <xref:System.IO.File.Decrypt%2A?displayProperty=fullName>
- <xref:System.IO.File.Delete%2A?displayProperty=fullName>
- <xref:System.IO.File.Encrypt%2A?displayProperty=fullName>
- <xref:System.IO.File.GetAttributes(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetCreationTime(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetCreationTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetLastAccessTime(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetLastAccessTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetLastWriteTime(System.String)?displayProperty=fullName>
- <xref:System.IO.File.GetLastWriteTimeUtc(System.String)?displayProperty=fullName>
- <xref:System.IO.File.Move%2A?displayProperty=fullName>
- <xref:System.IO.File.Open%2A?displayProperty=fullName>
- <xref:System.IO.File.OpenRead(System.String)?displayProperty=fullName>
- <xref:System.IO.File.OpenText(System.String)?displayProperty=fullName>
- <xref:System.IO.File.OpenWrite(System.String)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllBytes(System.String)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllBytesAsync(System.String,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllLines(System.String)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllLinesAsync(System.String,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllText(System.String)?displayProperty=fullName>
- <xref:System.IO.File.ReadAllTextAsync(System.String,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.IO.File.SetAttributes(System.String,System.IO.FileAttributes)?displayProperty=fullName>
- <xref:System.IO.File.SetCreationTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.SetCreationTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.SetLastAccessTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.SetLastAccessTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.SetLastWriteTime(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.SetLastWriteTimeUtc(System.String,System.DateTime)?displayProperty=fullName>
- <xref:System.IO.File.WriteAllBytes(System.String,System.Byte[])?displayProperty=fullName>
- <xref:System.IO.File.WriteAllBytesAsync(System.String,System.Byte[],System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.IO.File.WriteAllLines%2A?displayProperty=fullName>
- <xref:System.IO.File.WriteAllLinesAsync%2A?displayProperty=fullName>
- <xref:System.IO.File.WriteAllText%2A?displayProperty=fullName>
- <span data-ttu-id="c3e41-116">[System.IO.FileInfo ctor](xref:System.IO.FileInfo.%23ctor(System.String))</span><span class="sxs-lookup"><span data-stu-id="c3e41-116">[System.IO.FileInfo ctor](xref:System.IO.FileInfo.%23ctor(System.String))</span></span>
- <xref:System.IO.FileInfo.CopyTo%2A?displayProperty=fullName>
- <xref:System.IO.FileInfo.MoveTo%2A?displayProperty=fullName>
- [<span data-ttu-id="c3e41-117">System.IO.FileStream ctor</span><span class="sxs-lookup"><span data-stu-id="c3e41-117">System.IO.FileStream ctor</span></span>](xref:System.IO.FileStream.%23ctor%2A)
- <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.IsPathRooted(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.GetPathRoot(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.ChangeExtension(System.String,System.String)?displayProperty=fullName>
- <xref:System.IO.Path.GetDirectoryName(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.GetExtension(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.HasExtension(System.String)?displayProperty=fullName>
- <xref:System.IO.Path.Combine%2A?displayProperty=fullName>

#### <a name="see-also"></a><span data-ttu-id="c3e41-118">関連項目</span><span class="sxs-lookup"><span data-stu-id="c3e41-118">See also</span></span>

- [<span data-ttu-id="c3e41-119">.NET Core 2.1 の System.IO の先行プレビュー</span><span class="sxs-lookup"><span data-stu-id="c3e41-119">System.IO in .NET Core 2.1 sneak peek</span></span>](/archive/blogs/jeremykuhne/system-io-in-net-core-2-1-sneak-peek)

<!--

### Category

Core .NET libraries

### Affected APIs

- `Overload:System.IO.Directory.CreateDirectory`
- `Overload:System.IO.Directory.Delete`
- `Overload:System.IO.Directory.EnumerateDirectories`
- `Overload:System.IO.Directory.EnumerateFiles`
- `Overload:System.IO.Directory.EnumerateFileSystemEntries`
- `M:System.IO.Directory.GetCreationTime(System.String)`
- `M:System.IO.Directory.GetCreationTimeUtc(System.String)`
- `Overload:System.IO.Directory.GetDirectories`
- `M:System.IO.Directory.GetDirectoryRoot(System.String)`
- `Overload:System.IO.Directory.GetFiles`
- `Overload:System.IO.Directory.GetFileSystemEntries`
- `M:System.IO.Directory.GetLastAccessTime(System.String)`
- `M:System.IO.Directory.GetLastAccessTimeUtc(System.String)`
- `M:System.IO.Directory.GetLastWriteTime(System.String)`
- `M:System.IO.Directory.GetLastWriteTimeUtc(System.String)`
- `M:System.IO.Directory.GetParent(System.String)`
- `M:System.IO.Directory.Move(System.String,System.String)`
- `M:System.IO.Directory.SetCreationTime(System.String)`
- `M:System.IO.Directory.SetCreationTimeUtc(System.String)`
- `M:System.IO.Directory.SetCurrentDirectory(System.String)`
- `M:System.IO.Directory.SetLastAccessTime(System.String)`
- `M:System.IO.Directory.SetLastAccessTimeUtc(System.String)`
- `M:System.IO.Directory.SetLastWriteTime(System.String)`
- `M:System.IO.Directory.SetLastWriteTimeUtc(System.String)`
- `M:System.IO.DirectoryInfo.%23ctor(System.String)>
- `Overload:System.IO.Directory.GetDirectories`
- `Overload:System.IO.Directory.GetFiles`
- `Overload:System.IO.DirectoryInfo.GetFileSystemInfos`
- `Overload:System.IO.File.AppendAllText`
- `Overload:System.IO.File.AppendAllTextAsync`
- `Overload:System.IO.File.Copy`
- `Overload:System.IO.File.Create`
- `Overload:System.IO.File.CreateText`
- `Overload:System.IO.File.Decrypt`
- `Overload:System.IO.File.Delete`
- `Overload:System.IO.File.Encrypt`
- `M:System.IO.File.GetAttributes(System.String)`
- `M:System.IO.File.GetCreationTime(System.String)`
- `M:System.IO.File.GetCreationTimeUtc(System.String)`
- `M:System.IO.File.GetLastAccessTime(System.String)`
- `M:System.IO.File.GetLastAccessTimeUtc(System.String)`
- `M:System.IO.File.GetLastWriteTime(System.String)`
- `M:System.IO.File.GetLastWriteTimeUtc(System.String)`
- `Overload:System.IO.File.Move`
- `Overload:System.IO.File.Open`
- `M:System.IO.File.OpenRead(System.String)`
- `M:System.IO.File.OpenText(System.String)`
- `M:System.IO.File.OpenWrite(System.String)`
- `M:System.IO.File.ReadAllBytes(System.String)`
- `M:System.IO.File.ReadAllBytesAsync(System.String,System.Threading.CancellationToken)`
- `M:System.IO.File.ReadAllLines(System.String)`
- `M:System.IO.File.ReadAllLinesAsync(System.String,System.Threading.CancellationToken)`
- `M:System.IO.File.ReadAllText(System.String)`
- `M:System.IO.File.ReadAllTextAsync(System.String,System.Threading.CancellationToken)`
- `M:System.IO.File.SetAttributes(System.String)`
- `M:System.IO.File.SetCreationTime(System.String)`
- `M:System.IO.File.SetCreationTimeUtc(System.String)`
- `M:System.IO.File.SetLastAccessTime(System.String)`
- `M:System.IO.File.SetLastAccessTimeUtc(System.String)`
- `M:System.IO.File.SetLastWriteTime(System.String)`
- `M:System.IO.File.SetLastWriteTimeUtc(System.String)`
- `M:System.IO.File.WriteAllBytes(System.String)`
- `M:System.IO.File.WriteAllBytesAsync(System.String,System.Threading.CancellationToken)`
- `Overload:System.IO.File.WriteAllLines`
- `Overload:System.IO.File.WriteAllLinesAsync`
- `Overload:System.IO.File.WriteAllText`
- `M:System.IO.FileInfo.#ctor(System.String)`
- `Overload:System.IO.FileInfo.CopyTo`
- `Overload:System.IO.FileInfo.MoveTo`
- `Overload:System.IO.FileStream.#ctor`
- `M:System.IO.Path.GetFullPath(System.String)`
- `M:System.IO.Path.IsPathRooted(System.String)`
- `M:System.IO.Path.GetPathRoot(System.String)`
- `M:System.IO.Path.ChangeExtension(System.String,System.String)`
- `M:System.IO.Path.GetDirectoryName(System.String)`
- `M:System.IO.Path.GetExtension(System.String)`
- `M:System.IO.Path.HasExtension(System.String)`
- `Overload:System.IO.Path.Combine`

-->
