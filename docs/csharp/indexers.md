---
title: インデクサー
description: C# のインデクサーとインデックス付きプロパティの実装方法を説明します。これらのプロパは、1 つまたは複数の引数を使用して参照されます。
ms.date: 06/20/2016
ms.technology: csharp-fundamentals
ms.assetid: 0e9496da-e766-45a9-b92b-91820d4a350e
ms.openlocfilehash: 2efd8735587c35be8e89dba7499a0a661796067d
ms.sourcegitcommit: c7f0beaa2bd66ebca86362ca17d673f7e8256ca6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104875786"
---
# <a name="indexers"></a><span data-ttu-id="44170-103">インデクサー</span><span class="sxs-lookup"><span data-stu-id="44170-103">Indexers</span></span>

<span data-ttu-id="44170-104">"*インデクサー*" はプロパティに似ています。</span><span class="sxs-lookup"><span data-stu-id="44170-104">*Indexers* are similar to properties.</span></span> <span data-ttu-id="44170-105">さまざまな面で、インデクサーは[プロパティ](properties.md)と同じ言語機能を基にして構築されています。</span><span class="sxs-lookup"><span data-stu-id="44170-105">In many ways indexers build on the same language features as [properties](properties.md).</span></span> <span data-ttu-id="44170-106">インデクサーにより、"*インデックス付き*" プロパティを使用できるようになります。これは、1 つ以上の引数を使用して参照されるプロパティです。</span><span class="sxs-lookup"><span data-stu-id="44170-106">Indexers enable *indexed* properties: properties referenced using one or more arguments.</span></span> <span data-ttu-id="44170-107">これらの引数は、値のいくつかのコレクションにインデックスを提供します。</span><span class="sxs-lookup"><span data-stu-id="44170-107">Those arguments provide an index into some collection of values.</span></span>

## <a name="indexer-syntax"></a><span data-ttu-id="44170-108">インデクサーの構文</span><span class="sxs-lookup"><span data-stu-id="44170-108">Indexer Syntax</span></span>

<span data-ttu-id="44170-109">インデクサーにアクセスするには、変数名と角かっこを使用します。</span><span class="sxs-lookup"><span data-stu-id="44170-109">You access an indexer through a variable name and square brackets.</span></span> <span data-ttu-id="44170-110">インデクサーの引数は、角かっこで囲みます。</span><span class="sxs-lookup"><span data-stu-id="44170-110">You place the indexer arguments inside the brackets:</span></span>

```csharp
var item = someObject["key"];
someObject["AnotherKey"] = item;
```

<span data-ttu-id="44170-111">インデクサーを宣言するには、`this` キーワードをプロパティ名として使用し、引数を各かっこの中で宣言します。</span><span class="sxs-lookup"><span data-stu-id="44170-111">You declare indexers using the `this` keyword as the property name, and declaring the arguments within square brackets.</span></span> <span data-ttu-id="44170-112">この宣言は、前の段落で説明した使用方法と一致します。</span><span class="sxs-lookup"><span data-stu-id="44170-112">This declaration would match the usage shown in the previous paragraph:</span></span>

```csharp
public int this[string key]
{
    get { return storage.Find(key); }
    set { storage.SetAt(key, value); }
}
```

<span data-ttu-id="44170-113">この最初の例から、プロパティの構文とインデクサーの構文の関係がわかります。</span><span class="sxs-lookup"><span data-stu-id="44170-113">From this initial example, you can see the relationship between the syntax for properties and for indexers.</span></span> <span data-ttu-id="44170-114">この類似点は、インデクサーの構文規則のほとんどで見られます。</span><span class="sxs-lookup"><span data-stu-id="44170-114">This analogy carries through most of the syntax rules for indexers.</span></span> <span data-ttu-id="44170-115">インデクサーは、有効なアクセス修飾子 (public、protected internal、protected、internal、private、private protected) を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="44170-115">Indexers can have any valid access modifiers (public, protected internal, protected, internal, private or private protected).</span></span> <span data-ttu-id="44170-116">sealed、virtual、または abstract を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="44170-116">They may be sealed, virtual, or abstract.</span></span> <span data-ttu-id="44170-117">プロパティと同様に、インデクサーの get アクセサーと set アクセサーには異なるアクセス修飾子を指定できます。</span><span class="sxs-lookup"><span data-stu-id="44170-117">As with properties, you can specify different access modifiers for the get and set accessors in an indexer.</span></span>
<span data-ttu-id="44170-118">また、読み取り専用インデクサー (set アクセサーを省略) または書き込み専用インデクサー (get アクセサーを省略) を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="44170-118">You may also specify read-only indexers (by omitting the set accessor), or write-only indexers (by omitting the get accessor).</span></span>

<span data-ttu-id="44170-119">プロパティの操作方法から習得したほとんどすべてのことをインデクサーにも適用できます。</span><span class="sxs-lookup"><span data-stu-id="44170-119">You can apply almost everything you learn from working with properties to indexers.</span></span> <span data-ttu-id="44170-120">その唯一の例外は、"*自動実装プロパティ*" です。</span><span class="sxs-lookup"><span data-stu-id="44170-120">The only exception to that rule is *auto implemented properties*.</span></span> <span data-ttu-id="44170-121">コンパイラは、必ずしもインデクサーに適切なストレージを生成できるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="44170-121">The compiler cannot always generate the correct storage for an indexer.</span></span>

<span data-ttu-id="44170-122">項目のセット内の項目を参照するための引数が存在することも、インデクサーとプロパティの違いです。</span><span class="sxs-lookup"><span data-stu-id="44170-122">The presence of arguments to reference an item in a set of items distinguishes indexers from properties.</span></span> <span data-ttu-id="44170-123">インデクサーごとの引数リストが一意である場合は、1 つの型に複数のインデクサーを定義できます。</span><span class="sxs-lookup"><span data-stu-id="44170-123">You may define multiple indexers on a type, as long as the argument lists for each indexer is unique.</span></span> <span data-ttu-id="44170-124">それでは、クラス定義で 1 つ以上のインデクサーを使用するさまざまなシナリオを見ていきましょう。</span><span class="sxs-lookup"><span data-stu-id="44170-124">Let's explore different scenarios where you might use one or more indexers in a class definition.</span></span>

## <a name="scenarios"></a><span data-ttu-id="44170-125">シナリオ</span><span class="sxs-lookup"><span data-stu-id="44170-125">Scenarios</span></span>

<span data-ttu-id="44170-126">型の API がコレクションをモデル化していて、そのコレクションへの引数が定義されている場合に、型に "*インデクサー*" を定義します。</span><span class="sxs-lookup"><span data-stu-id="44170-126">You would define *indexers* in your type when its API models some collection where you define the arguments to that collection.</span></span> <span data-ttu-id="44170-127">インデクサーは、.NET Core Framework に含まれているコレクション型に直接マップされることもあれば、されないこともあります。</span><span class="sxs-lookup"><span data-stu-id="44170-127">Your indexers may or may not map directly to the collection types that are part of the .NET core framework.</span></span> <span data-ttu-id="44170-128">型は、コレクションのモデル化だけでなく、他の役割がある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="44170-128">Your type may have other responsibilities in addition to modeling a collection.</span></span>
<span data-ttu-id="44170-129">インデクサーを使用すると、型の抽象化に適した API を提供することができ、抽象化された値の格納や計算の方法の内部の詳細を公開しなくて済みます。</span><span class="sxs-lookup"><span data-stu-id="44170-129">Indexers enable you to provide the API that matches your type's abstraction without exposing the inner details of how the values for that abstraction are stored or computed.</span></span>

<span data-ttu-id="44170-130">"*インデクサー*" を使用する一般的なシナリオをいくつか見ていきましょう。</span><span class="sxs-lookup"><span data-stu-id="44170-130">Let's walk through some of the common scenarios for using *indexers*.</span></span> <span data-ttu-id="44170-131">[インデクサーのサンプル フォルダー](https://github.com/dotnet/samples/tree/main/csharp/indexers)にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="44170-131">You can access the [sample folder for indexers](https://github.com/dotnet/samples/tree/main/csharp/indexers).</span></span> <span data-ttu-id="44170-132">ダウンロード方法については、「[サンプルおよびチュートリアル](../samples-and-tutorials/index.md#view-and-download-samples)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44170-132">For download instructions, see [Samples and Tutorials](../samples-and-tutorials/index.md#view-and-download-samples).</span></span>

### <a name="arrays-and-vectors"></a><span data-ttu-id="44170-133">配列とベクター</span><span class="sxs-lookup"><span data-stu-id="44170-133">Arrays and Vectors</span></span>

<span data-ttu-id="44170-134">インデクサーを作成する最も一般的なシナリオの 1 つは、型が配列またはベクターをモデル化する場合です。</span><span class="sxs-lookup"><span data-stu-id="44170-134">One of the most common scenarios for creating indexers is when your type models an array, or a vector.</span></span> <span data-ttu-id="44170-135">データの番号付きリストをモデル化するためのインデクサーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="44170-135">You can create an indexer to model an ordered list of data.</span></span>

<span data-ttu-id="44170-136">独自のインデクサーを作成する利点は、ニーズに合わせてそのコレクションのストレージを定義できることです。</span><span class="sxs-lookup"><span data-stu-id="44170-136">The advantage of creating your own indexer is that you can define the storage for that collection to suit your needs.</span></span> <span data-ttu-id="44170-137">一度でメモリに読み込むには大きすぎる履歴データを型でモデル化するシナリオを考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="44170-137">Imagine a scenario where your type models historical data that is too large to load into memory at once.</span></span> <span data-ttu-id="44170-138">使用状況に基づいて、コレクションのセクションを読み込んだりアンロードしたりする必要があります。</span><span class="sxs-lookup"><span data-stu-id="44170-138">You need to load and unload sections of the collection based on usage.</span></span> <span data-ttu-id="44170-139">次の例では、この動作をモデル化します。</span><span class="sxs-lookup"><span data-stu-id="44170-139">The example following models this behavior.</span></span> <span data-ttu-id="44170-140">存在するデータ ポイント数が報告されます。</span><span class="sxs-lookup"><span data-stu-id="44170-140">It reports on how many data points exist.</span></span> <span data-ttu-id="44170-141">必要に応じて、データのセクションを保持するページを作成します。</span><span class="sxs-lookup"><span data-stu-id="44170-141">It creates pages to hold sections of the data on demand.</span></span> <span data-ttu-id="44170-142">より新しい要求によって必要とされるページのための領域を確保するために、メモリからページを削除します。</span><span class="sxs-lookup"><span data-stu-id="44170-142">It removes pages from memory to make room for pages needed by more recent requests.</span></span>

```csharp
public class DataSamples
{
    private class Page
    {
        private readonly List<Measurements> pageData = new List<Measurements>();
        private readonly int startingIndex;
        private readonly int length;
        private bool dirty;
        private DateTime lastAccess;

        public Page(int startingIndex, int length)
        {
            this.startingIndex = startingIndex;
            this.length = length;
            lastAccess = DateTime.Now;

            // This stays as random stuff:
            var generator = new Random();
            for(int i=0; i < length; i++)
            {
                var m = new Measurements
                {
                    HiTemp = generator.Next(50, 95),
                    LoTemp = generator.Next(12, 49),
                    AirPressure = 28.0 + generator.NextDouble() * 4
                };
                pageData.Add(m);
            }
        }
        public bool HasItem(int index) =>
            ((index >= startingIndex) &&
            (index < startingIndex + length));

        public Measurements this[int index]
        {
            get
            {
                lastAccess = DateTime.Now;
                return pageData[index - startingIndex];
            }
            set
            {
                pageData[index - startingIndex] = value;
                dirty = true;
                lastAccess = DateTime.Now;
            }
        }

        public bool Dirty => dirty;
        public DateTime LastAccess => lastAccess;
    }

    private readonly int totalSize;
    private readonly List<Page> pagesInMemory = new List<Page>();

    public DataSamples(int totalSize)
    {
        this.totalSize = totalSize;
    }

    public Measurements this[int index]
    {
        get
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");

            var page = updateCachedPagesForAccess(index);
            return page[index];
        }
        set
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");
            var page = updateCachedPagesForAccess(index);

            page[index] = value;
        }
    }

    private Page updateCachedPagesForAccess(int index)
    {
        foreach (var p in pagesInMemory)
        {
            if (p.HasItem(index))
            {
                return p;
            }
        }
        var startingIndex = (index / 1000) * 1000;
        var newPage = new Page(startingIndex, 1000);
        addPageToCache(newPage);
        return newPage;
    }

    private void addPageToCache(Page p)
    {
        if (pagesInMemory.Count > 4)
        {
            // remove oldest non-dirty page:
            var oldest = pagesInMemory
                .Where(page => !page.Dirty)
                .OrderBy(page => page.LastAccess)
                .FirstOrDefault();
            // Note that this may keep more than 5 pages in memory
            // if too much is dirty
            if (oldest != null)
                pagesInMemory.Remove(oldest);
        }
        pagesInMemory.Add(p);
    }
}
```

<span data-ttu-id="44170-143">この設計手法に従って、メモリ内コレクションにデータのセット全体を読み込まないことが妥当であるような種類のコレクションをモデル化できます。</span><span class="sxs-lookup"><span data-stu-id="44170-143">You can follow this design idiom to model any sort of collection where there are good reasons not to load the entire set of data into an in- memory collection.</span></span> <span data-ttu-id="44170-144">`Page` クラスが、パブリック インターフェイスの一部ではない、入れ子になったプライベート クラスであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44170-144">Notice that the `Page` class is a private nested class that is not part of the public interface.</span></span> <span data-ttu-id="44170-145">これらの詳細は、このクラスのユーザーには表示されません。</span><span class="sxs-lookup"><span data-stu-id="44170-145">Those details are hidden from any users of this class.</span></span>

### <a name="dictionaries"></a><span data-ttu-id="44170-146">ディクショナリ</span><span class="sxs-lookup"><span data-stu-id="44170-146">Dictionaries</span></span>

<span data-ttu-id="44170-147">もう 1 つの一般的なシナリオは、ディクショナリまたはマップをモデル化する必要がある場合です。</span><span class="sxs-lookup"><span data-stu-id="44170-147">Another common scenario is when you need to model a dictionary or a map.</span></span> <span data-ttu-id="44170-148">このシナリオでは、キー (通常はテキスト キー) に基づいて型が値を格納します。</span><span class="sxs-lookup"><span data-stu-id="44170-148">This scenario is when your type stores values based on key, typically text keys.</span></span> <span data-ttu-id="44170-149">この例では、これらのオプションを管理する[ラムダ式](delegates-overview.md)にコマンド ライン引数をマップするディクショナリを作成します。</span><span class="sxs-lookup"><span data-stu-id="44170-149">This example creates a dictionary that maps command line arguments to [lambda expressions](delegates-overview.md) that manage those options.</span></span> <span data-ttu-id="44170-150">次の例では、2 つのクラスを示します。`ArgsActions` クラスは、コマンド ライン オプションを `Action` デリゲートにマップします。`ArgsProcessor` クラスは、そのオプションが検出されたときに、`ArgsActions` を使用して各 `Action` を実行します。</span><span class="sxs-lookup"><span data-stu-id="44170-150">The following example shows two classes: an `ArgsActions` class that maps a command line option to an `Action` delegate, and an `ArgsProcessor` that uses the `ArgsActions` to execute each `Action` when it encounters that option.</span></span>

```csharp
public class ArgsProcessor
{
    private readonly ArgsActions actions;

    public ArgsProcessor(ArgsActions actions)
    {
        this.actions = actions;
    }

    public void Process(string[] args)
    {
        foreach(var arg in args)
        {
            actions[arg]?.Invoke();
        }
    }

}
public class ArgsActions
{
    readonly private Dictionary<string, Action> argsActions = new Dictionary<string, Action>();

    public Action this[string s]
    {
        get
        {
            Action action;
            Action defaultAction = () => {} ;
            return argsActions.TryGetValue(s, out action) ? action : defaultAction;
        }
    }

    public void SetOption(string s, Action a)
    {
        argsActions[s] = a;
    }
}
```

<span data-ttu-id="44170-151">この例では、`ArgsAction` コレクションが、基になるコレクションと密接に対応しています。</span><span class="sxs-lookup"><span data-stu-id="44170-151">In this example, the `ArgsAction` collection maps closely to the underlying collection.</span></span>
<span data-ttu-id="44170-152">`get` は、特定のオプションが構成されているかどうかを判定します。</span><span class="sxs-lookup"><span data-stu-id="44170-152">The `get` determines if a given option has been configured.</span></span> <span data-ttu-id="44170-153">構成されている場合は、そのオプションに関連付けられている `Action` が返されます。</span><span class="sxs-lookup"><span data-stu-id="44170-153">If so, it returns the `Action` associated with that option.</span></span> <span data-ttu-id="44170-154">構成されていない場合は、何も実行しない `Action` が返されます。</span><span class="sxs-lookup"><span data-stu-id="44170-154">If not, it returns an `Action` that does nothing.</span></span> <span data-ttu-id="44170-155">パブリック アクセサーには、`set` アクセサーは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="44170-155">The public accessor does not include a `set` accessor.</span></span> <span data-ttu-id="44170-156">代わりに、オプションの設定にパブリック メソッドを使用する設計になっています。</span><span class="sxs-lookup"><span data-stu-id="44170-156">Rather, the design using a public method for setting options.</span></span>

### <a name="multi-dimensional-maps"></a><span data-ttu-id="44170-157">多次元マップ</span><span class="sxs-lookup"><span data-stu-id="44170-157">Multi-Dimensional Maps</span></span>

<span data-ttu-id="44170-158">複数の引数を使用するインデクサーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="44170-158">You can create indexers that use multiple arguments.</span></span> <span data-ttu-id="44170-159">さらに、これらの引数は、同じ型でなくてもかまいません。</span><span class="sxs-lookup"><span data-stu-id="44170-159">In addition, those arguments are not constrained to be the same type.</span></span> <span data-ttu-id="44170-160">2 つの例を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="44170-160">Let's look at two examples.</span></span>

<span data-ttu-id="44170-161">最初の例は、マンデルブロ集合の値を生成するクラスを示しています。</span><span class="sxs-lookup"><span data-stu-id="44170-161">The first example shows a class that generates values for a Mandelbrot set.</span></span> <span data-ttu-id="44170-162">集合の数学的な背景情報の詳細については、[こちらの記事](https://en.wikipedia.org/wiki/Mandelbrot_set)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44170-162">For more information on the mathematics behind the set, read [this article](https://en.wikipedia.org/wiki/Mandelbrot_set).</span></span>
<span data-ttu-id="44170-163">インデクサーは、2 つの倍精度浮動小数点数を使用して、X および Y 平面上の点を定義します。</span><span class="sxs-lookup"><span data-stu-id="44170-163">The indexer uses two doubles to define a point in the X, Y plane.</span></span>
<span data-ttu-id="44170-164">get アクセサーは、点が集合内に存在しないと判断されるまで、イテレーションの回数を計算します。</span><span class="sxs-lookup"><span data-stu-id="44170-164">The get accessor computes the number of iterations until a point is determined to be not in the set.</span></span> <span data-ttu-id="44170-165">イテレーションの最大数に達した場合、点は集合内に存在し、クラスの maxIterations 値が返されます。</span><span class="sxs-lookup"><span data-stu-id="44170-165">If the maximum iterations is reached, the point is in the set, and the class's maxIterations value is returned.</span></span> <span data-ttu-id="44170-166">マンデルブロ集合でよく知られている、コンピューターで生成される画像では、点が集合外に存在すると判断するために必要なイテレーションの数に対して色を定義します。</span><span class="sxs-lookup"><span data-stu-id="44170-166">(The computer generated images popularized for the Mandelbrot set define colors for the number of iterations necessary to determine that a point is outside the set.</span></span>

```csharp
public class Mandelbrot
{
    readonly private int maxIterations;

    public Mandelbrot(int maxIterations)
    {
        this.maxIterations = maxIterations;
    }

    public int this [double x, double y]
    {
        get
        {
            var iterations = 0;
            var x0 = x;
            var y0 = y;

            while ((x*x + y * y < 4) &&
                (iterations < maxIterations))
            {
                var newX = x * x - y * y + x0;
                y = 2 * x * y + y0;
                x = newX;
                iterations++;
            }
            return iterations;
        }
    }
}
```

<span data-ttu-id="44170-167">マンデルブロ集合では、実数値の各 (x,y) 座標の値を定義します。</span><span class="sxs-lookup"><span data-stu-id="44170-167">The Mandelbrot Set defines values at every (x,y) coordinate for real number values.</span></span>
<span data-ttu-id="44170-168">これによって、無限の数の値を格納できるディクショナリが定義されます。</span><span class="sxs-lookup"><span data-stu-id="44170-168">That defines a dictionary that could contain an infinite number of values.</span></span> <span data-ttu-id="44170-169">そのため、集合の背後にストレージはありません。</span><span class="sxs-lookup"><span data-stu-id="44170-169">Therefore, there is no storage behind the set.</span></span> <span data-ttu-id="44170-170">代わりに、このクラスはコードが `get` アクセサーを呼び出すときに各点の値を計算します。</span><span class="sxs-lookup"><span data-stu-id="44170-170">Instead, this class computes the value for each point when code calls the `get` accessor.</span></span> <span data-ttu-id="44170-171">使用される、基になるストレージはありません。</span><span class="sxs-lookup"><span data-stu-id="44170-171">There's no underlying storage used.</span></span>

<span data-ttu-id="44170-172">最後の使用例を調べてみましょう。この例では、インデクサーが異なる型の複数の引数を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="44170-172">Let's examine one last use of indexers, where the indexer takes multiple arguments of different types.</span></span> <span data-ttu-id="44170-173">気温の履歴データを管理するプログラムがあるとします。</span><span class="sxs-lookup"><span data-stu-id="44170-173">Consider a program that manages historical temperature data.</span></span> <span data-ttu-id="44170-174">このインデクサーは、市区町村と日付を使用して、その場所の最高気温と最低気温を設定または取得します。</span><span class="sxs-lookup"><span data-stu-id="44170-174">This indexer uses a city and a date to set or get the high and low temperatures for that location:</span></span>

```csharp
using DateMeasurements =
    System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements =
    System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;

public class HistoricalWeatherData
{
    readonly CityDataMeasurements storage = new CityDataMeasurements();

    public Measurements this[string city, DateTime date]
    {
        get
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
                throw new ArgumentOutOfRangeException(nameof(city), "City not found");

            // strip out any time portion:
            var index = date.Date;
            var measure = default(Measurements);
            if (cityData.TryGetValue(index, out measure))
                return measure;
            throw new ArgumentOutOfRangeException(nameof(date), "Date not found");
        }
        set
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
            {
                cityData = new DateMeasurements();
                storage.Add(city, cityData);
            }

            // Strip out any time portion:
            var index = date.Date;
            cityData[index] = value;
        }
    }
}
```

<span data-ttu-id="44170-175">この例では、気象データを 2 つの異なる引数にマップするインデクサーを作成します。その引数は、city (`string` で表されます) と date (`DateTime` で表されます) です。</span><span class="sxs-lookup"><span data-stu-id="44170-175">This example creates an indexer that maps weather data on two different arguments: a city (represented by a `string`) and a date (represented by a `DateTime`).</span></span> <span data-ttu-id="44170-176">内部ストレージでは、2 つの `Dictionary` クラスを使用して、2 次元ディクショナリを表します。</span><span class="sxs-lookup"><span data-stu-id="44170-176">The internal storage uses two `Dictionary` classes to represent the two-dimensional dictionary.</span></span> <span data-ttu-id="44170-177">パブリック API は、基になるストレージを表さなくなります。</span><span class="sxs-lookup"><span data-stu-id="44170-177">The public API no longer represents the underlying storage.</span></span> <span data-ttu-id="44170-178">代わりに、インデクサーの言語機能を使用すると、基になるストレージで別の主要コレクション型を使用する必要があっても、抽象化を表すパブリック インターフェイスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="44170-178">Rather, the language features of indexers enables you to create a public interface that represents your abstraction, even though the underlying storage must use different core collection types.</span></span>

<span data-ttu-id="44170-179">このコードには、一部の開発者にはなじみのない部分が 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="44170-179">There are two parts of this code that may be unfamiliar to some developers.</span></span> <span data-ttu-id="44170-180">これら 2 つの `using` ディレクティブです。</span><span class="sxs-lookup"><span data-stu-id="44170-180">These two `using` directives:</span></span>

```csharp
using DateMeasurements = System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements = System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;
```

<span data-ttu-id="44170-181">構築ジェネリック型の "*エイリアス*" を作成しています。</span><span class="sxs-lookup"><span data-stu-id="44170-181">create an *alias* for a constructed generic type.</span></span> <span data-ttu-id="44170-182">これらのステートメントにより、後のコードでは、`Dictionary<DateTime, Measurements>` と `Dictionary<string, Dictionary<DateTime, Measurements> >` のジェネリック コンストラクションではなく、よりわかりやすい `DateMeasurements` と `CityDateMeasurements` という名前を使用できます。</span><span class="sxs-lookup"><span data-stu-id="44170-182">Those statements enable the code later to use the more descriptive `DateMeasurements` and `CityDateMeasurements` names instead of the generic construction of `Dictionary<DateTime, Measurements>` and `Dictionary<string, Dictionary<DateTime, Measurements> >`.</span></span>
<span data-ttu-id="44170-183">このコンストラクトでは、`=` 記号の右辺で完全修飾型名を使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="44170-183">This construct does require using the fully qualified type names on the right side of the `=` sign.</span></span>

<span data-ttu-id="44170-184">2 つ目の手法では、コレクションへのインデックス作成に使用された任意の `DateTime` オブジェクトから時間部分を取り除きます。</span><span class="sxs-lookup"><span data-stu-id="44170-184">The second technique is to strip off the time portions of any `DateTime` object used to index into the collections.</span></span> <span data-ttu-id="44170-185">.NET には、日付のみの型は含まれません。</span><span class="sxs-lookup"><span data-stu-id="44170-185">.NET doesn't include a date-only type.</span></span>
<span data-ttu-id="44170-186">開発者は `DateTime` 型を使用しますが、`Date` プロパティを使用して、その日のすべての `DateTime` オブジェクトが等しくなるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="44170-186">Developers use the `DateTime` type, but use the `Date` property to ensure that any `DateTime` object from that day are equal.</span></span>

## <a name="summing-up"></a><span data-ttu-id="44170-187">まとめ</span><span class="sxs-lookup"><span data-stu-id="44170-187">Summing Up</span></span>

<span data-ttu-id="44170-188">クラスにプロパティのような要素があり、そのプロパティが単一の値ではなく値のコレクションを表していて、各項目が引数のセットによって識別される場合は、インデクサーを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44170-188">You should create indexers anytime you have a property-like element in your class where that property represents not a single value, but rather a collection of values where each individual item is identified by a set of arguments.</span></span> <span data-ttu-id="44170-189">これらの引数では、参照する必要があるコレクションの項目を一意に特定できます。</span><span class="sxs-lookup"><span data-stu-id="44170-189">Those arguments can uniquely identify which item in the collection should be referenced.</span></span>
<span data-ttu-id="44170-190">インデクサーにより、[プロパティ](properties.md)の概念は拡張されます。メンバーはクラスの外部からデータ項目のように扱われますが、内部ではメソッドに似ています。</span><span class="sxs-lookup"><span data-stu-id="44170-190">Indexers extend the concept of [properties](properties.md), where a member is treated like a data item from outside the class, but like a method on the inside.</span></span> <span data-ttu-id="44170-191">インデクサーを使用すると、引数は、項目のセットを表すプロパティ内で単一の項目を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="44170-191">Indexers allow arguments to find a single item in a property that represents a set of items.</span></span>
