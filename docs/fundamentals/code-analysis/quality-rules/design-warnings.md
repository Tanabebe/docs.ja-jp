---
title: デザイン規則 (コード分析)
description: コード分析デザイン規則について説明します。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.designrules
helpviewer_keywords:
- design rules
- managed code analysis rules, design rules
- rules, design
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 548e0eaaa6239a9b9ee6a08677cd720710bb48c2
ms.sourcegitcommit: 05d0087dfca85aac9ca2960f86c5efd218bf833f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2021
ms.locfileid: "99714132"
---
# <a name="design-rules"></a>デザイン規則

デザイン規則は、[.NET Framework デザイン ガイドライン](../../../standard/design-guidelines/index.md)の順守をサポートします。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1000:ジェネリック型の静的メンバーを宣言しません](ca1000.md) | ジェネリック型の静的メンバーを呼び出すときには、その型の型引数も指定する必要があります。 推論をサポートしないジェネリック インスタンス メンバーを呼び出すときには、そのメンバーに型引数を指定する必要があります。 この 2 つの場合、型引数を指定するときに使用される構文は異なりますが、混同される可能性があります。 |
| [CA1001:破棄可能なフィールドを所有する型は、破棄可能でなければなりません](ca1001.md) | クラスが System.IDisposable 型であるインスタンス フィールドを宣言および実装していますが、IDisposable を実装していません。 IDisposable フィールドを宣言するクラスは間接的にアンマネージ リソースを所有しているため、IDisposable インターフェイスを実装する必要があります。 |
| [CA1002:ジェネリック リストを公開しません](ca1002.md) | System.Collections.Generic.List<(Of \<(T>)>) は継承ではなくパフォーマンスを目的としたジェネリック コレクションです。 このため、List には仮想メンバーは含まれません。 代わりに、継承を目的としたジェネリック コレクションを公開する必要があります。 |
| [CA1003:汎用イベント ハンドラーのインスタンスを使用します](ca1003.md) | 型に void を返すデリゲートが含まれており、デリゲートのシグネチャに 2 つのパラメーター (1 つはオブジェクト、もう 1 つは EventArgs に割り当て可能な型) が含まれ、包含アセンブリの対象が .NET Framework 2.0. です。 |
| [CA1005:ジェネリック型でパラメーターを使用しすぎないでください](ca1005.md) | ジェネリック型に含まれる型パラメーターが増えれば増えるほど、それぞれの型パラメーターが表す意味を調べることや覚えることが難しくなります。 通常、List\<T> のように型パラメーターが 1 つの場合や、Dictionary\<TKey, TValue> のように型パラメーターが 2 つの場合、意味は明確です。 しかし、型パラメーターが 3 つ以上になると、ほとんどのユーザーには意味を把握することが困難になります。 |
| [CA1008:Enums は 0 値を含んでいなければなりません](ca1008.md) | 初期化されていない列挙型の既定値は、他の値型と同様に、ゼロです。 フラグではない属性が付いた列挙型では、ゼロの値を使用してメンバーを定義する必要があります。これは、既定値を有効な列挙値にするためです。 FlagsAttribute 属性を適用した列挙型でゼロ値のメンバーを定義する場合、名前を "None" にして、列挙型に設定済みの値がないことを示します。 |
| [CA1010:コレクションは、ジェネリック インターフェイスを実装しなければなりません](ca1010.md) | コレクションの操作性を拡充するために、ジェネリック コレクション インターフェイスの 1 つを実装します。 これにより、コレクションを使用してジェネリック コレクション型を設定できます。 |
| [CA1012:抽象型にはコンストラクターを含めません](ca1012.md) | 抽象型上のコンストラクターは、派生型からのみ呼び出すことができます。 パブリック コンストラクターで型のインスタンスが作成され、抽象型のインスタンスは自分で作成できないため、パブリック コンストラクターが含まれる抽象型のデザインは不適切になります。 |
| [CA1014:アセンブリに CLSCompliantAttribute を設定します](ca1014.md) | 共通言語仕様 (CLS) には、名前付けの制約、データ型、および規則が定義されています。アセンブリを複数のプログラミング言語で使用する場合、この仕様に準拠する必要があります。 すべてのアセンブリに CLSCompliantAttribute を使用して、CLS への準拠を明示することをお勧めします。 この属性が使用されていないアセンブリは、CLS に準拠しません。 |
| [CA1016:アセンブリに AssemblyVersionAttribute を設定します](ca1016.md) | .NET では、バージョン番号を使用してアセンブリを一意に識別し、厳密な名前を持つアセンブリの型にバインドします。 バージョン番号は、バージョンと発行者のポリシーと共に使用されます。 既定で、アプリケーションは、ビルドされたアセンブリのバージョンでのみ実行されます。 |
| [CA1017:アセンブリに ComVisibleAttribute を設定します](ca1017.md) | ComVisibleAttribute 属性によって、COM クライアントからマネージド コードにアクセスする方法が決まります。 アセンブリで COM の参照範囲を明示することをお勧めします。 COM の参照範囲は、アセンブリ全体に設定し、個々の型と型のメンバー用にオーバーライドできます。 この属性がない場合、アセンブリのコンテンツは COM クライアントから参照できます。 |
| [CA1018:属性を AttributeUsageAttribute に設定します](ca1018.md) | カスタム属性を定義する場合、AttributeUsageAttribute を使用してマークし、カスタム属性を適用できるソース コードの位置を示します。 属性の意味と用途によって、コード内の有効な位置が決まります。 |
| [CA1019:属性引数にアクセサーを定義します](ca1019.md) | 属性では、対象に適用するときに必ず指定する必須の引数を定義できます。 この引数は、コンストラクターに位置指定パラメーターで属性を指定できるようになるため、位置指定引数とも呼ばれます。 必須のすべての引数について、対応する読み取り専用のプロパティも属性で規定する必要があります。これは、引数値を実行時に取得できるようにするためです。 また、属性ではオプションの引数も定義できます。これは名前付き引数とも呼ばれます。 この引数は、名前でコンストラクターに属性を指定するときに使用されます。また、対応する読み取り/書き込みプロパティが必要です。 |
| [CA1021:out パラメーターを使用しません](ca1021.md) | (out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 また、out パラメーターと ref パラメーターの違いはあまり理解されていません。 |
| [CA1024:適切な場所にプロパティを使用します](ca1024.md) | パブリック メソッドまたはプロテクト メソッドに、"Get" で始まる名前が付けられ、パラメーターは使用されていません。また、配列ではない値を返します。 このメソッドは、プロパティに変更できる可能性があります。 |
| [CA1027:列挙型を FlagsAttribute に設定します](ca1027.md) | 列挙型は、関連する名前付き定数が複数定義された値型です。 名前付き定数を有意に結合できる場合、列挙型に FlagsAttribute を適用します。 |
| [CA1028:列挙ストレージは Int32 でなければなりません](ca1028.md) | 列挙型は、関連する名前付き定数が複数定義された値型です。 既定で、System.Int32 データ型は、定数値を格納するために使用されます。 この基になる型を変更できる場合でも、ほとんどの場合、変更する必要はなく、推奨もされません。 |
| [CA1030:適切な場所にイベントを使用します](ca1030.md) | この規則では、通常はイベントに使用される名前を持つメソッドを検出します。 明示的に定義された状態変化に応答してメソッドが呼び出される場合、メソッドはイベント ハンドラーから呼び出す必要があります。 メソッドを呼び出すオブジェクトは、メソッドを直接呼び出すのではなく、イベントを発生させる必要があります。 |
| [CA1031:一般的な例外の種類はキャッチしません](ca1031.md) | 汎用的な例外はキャッチしないでください。 より具体的な例外をキャッチするか、汎用的な例外を catch ブロックの最後のステートメントでスローし直します。 |
| [CA1032:標準例外コンストラクターを実装します](ca1032.md) | コンストラクターを完全に宣言していないと、例外を正しく処理するのが困難になります。 |
| [CA1033:インターフェイス メソッドは、子型によって呼び出し可能でなければなりません](ca1033.md) | シールされていない外部から参照できる型によって、パブリック インターフェイスを持つメソッドを明示的に実装しています。また、同じ名前を持つ外部から参照できる代替のメソッドがありません。 |
| [CA1034:入れ子にされた型を参照可能にすることはできません](ca1034.md) | 入れ子にされた型とは、別の型のスコープ内で宣言された型のことです。 入れ子にされた型は、包含型のプライベート実装の詳細をカプセル化するときに便利です。 このような用途なので、入れ子にされた型は外部から参照できないようにします。 |
| [CA1036:比較可能な型でメソッドをオーバーライドします](ca1036.md) | パブリック型またはプロテクト型で System.IComparable インターフェイスを実装しています。 これによって、Object.Equals はオーバーライドされません。また、"等しい"、"等しくない"、"未満"、"より大きい" を示す言語固有の演算子はオーバーロードされません。 |
| [CA1040:空のインターフェイスは使用しません](ca1040.md) | インターフェイスには、動作や使用のコントラクトを実現するメンバーが定義されます。 インターフェイスで示される機能は、継承の階層構造内に型が存在するかどうかにかかわらず、どの型からも適用できます。 型ではインターフェイスのメンバーに実装することで、インターフェイスが実装されます。 空のインターフェイスではメンバーが定義されません。そのため、実装できるコントラクトも定義されません。 |
| [CA1041:ObsoleteAttribute メッセージを指定します](ca1041.md) | 型またはメンバーが System.ObsoleteAttribute 属性を使用してマークされていますが、この属性で ObsoleteAttribute.Message プロパティが指定されていません。 ObsoleteAttribute でマークされている型またはメンバーをコンパイルすると、属性の Message プロパティが表示されます。これにより、互換性のために残されている型またはメンバーに関するユーザー情報が表示されます。 |
| [CA1043:インデクサーには整数または文字列引数を使用します](ca1043.md) | インデクサー (つまり、インデックスされたプロパティ) では、インデックスに整数型または文字列型を使用します。 一般に、このような型はデータ構造のインデックス作成に使用され、ライブラリの操作性も改善されます。 Object 型の使用は、デザイン時に特定の整数型または文字列型を指定できない場合に限定してください。 |
| [CA1044:プロパティを書き込み専用にすることはできません](ca1044.md) | 読み取り専用のプロパティは許容され、必要な場合もよくありますが、書き込み専用のプロパティを使用することはデザインのガイドラインで禁止されています。 これは、値を設定できてもその値を参照できず、セキュリティが確保されないためです。 また、読み取りアクセスがないと、共有オブジェクトのステータスを参照できないため、実用性が制限されます。 |
| [CA1045:型を参照によって渡しません](ca1045.md) | (out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 開発者全般に向けてライブラリをデザインする場合、ユーザーが out パラメーターまたは ref パラメーターの扱い方を習得することは期待しないでください。 |
| [CA1046:参照型で、演算子 equals をオーバーロードしないでください](ca1046.md) | 参照型の場合、等値演算子は既定の実装でほぼ問題がありません。 既定で、2 つの参照が等値と見なされるのは、同じオブジェクトを参照する場合のみです。 |
| [CA1047:シールド型の保護されたメンバーを宣言しません](ca1047.md) | 型でプロテクト メンバーを宣言するのは、継承する型からメンバーにアクセスまたはオーバーライドできるようにするためです。 定義により、シールされた型から継承することはできません。これは、シールされた型のプロテクト メソッドを呼び出すことができないということを意味します。 |
| [CA1050:名前空間で型を宣言します](ca1050.md) | 型を名前空間内で宣言するのは、名前が衝突しないようにするためと、関連する型をオブジェクト階層形式で編成するためです。 |
| [CA1051:参照可能なインスタンス フィールドを宣言しません](ca1051.md) | フィールドの主な用途は、実装の詳細にする必要があります。 フィールドは private または internal にし、プロパティによって公開するようにします。 |
| [CA1052:スタティック ホルダー型はシールドされていなければなりません](ca1052.md) | パブリック型またはプロテクト型に静的メンバーしかなく、sealed (C#) または NotInheritable (Visual Basic) 修飾子を使用して宣言されていません。 継承を意図していない型は、sealed 修飾子を使用してマークし、基本型として使用できないようにします。 |
| [CA1053:スタティック ホルダー型はコンストラクターを含むことはできません](ca1053.md) | パブリック型または入れ子になったパブリック型で、静的なメンバーのみが宣言されています。また、パブリックまたはプロテクトの既定のコンストラクターが含まれます。 静的メンバーの呼び出しに型のインスタンスは必要ないため、コンストラクターは不要です。 安全性とセキュリティを確保するために、文字列引数を使用して文字列オーバーロードで URI (Uniform Resource Identifier) オーバーロードを呼び出してください。 |
| [CA1054:URI パラメーターを文字列にすることはできません](ca1054.md) | メソッドで URI の文字列形式を使用する場合、対応するオーバーロードを宣言し、URI クラスのインスタンスを使用します。こうすることで、安全な方法でこのサービスを実現できます。 |
| [CA1055:URI 戻り値を文字列にすることはできません](ca1055.md) | この規則では、メソッドは URI を返すと想定されます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。 |
| [CA1056:URI プロパティを文字列にすることはできません](ca1056.md) | この規則では、プロパティは URI を表すと想定されます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。 |
| [CA1058:型は、一定の基本型を拡張することはできません](ca1058.md) | 外部から参照可能な型では、特定の基本型が拡張されます。 別の型を使用してください。 |
| [CA1060: P/Invoke を NativeMethods クラスに移動します](ca1060.md) | <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> でマークされているものなどのプラットフォーム呼び出しメソッド、または Visual Basic で Declare キーワードを使用して定義されているメソッドから、アンマネージド コードにアクセスしています。 これらのメソッドは、NativeMethods、SafeNativeMethods、UnsafeNativeMethods の各クラスのいずれかに含まれる必要があります。 |
| [CA1061:基底クラス メソッドを非表示にしません](ca1061.md) | 派生メソッドのパラメーター シグネチャ内のある型が、基本メソッドのパラメーター シグネチャ内のそれに対応する型より弱く型指定されていることが、両者の唯一の相違点である場合、基本型内のメソッドが派生型内の同じ名前のメソッドによって隠ぺいされます。 |
| [CA1062:パブリック メソッドの引数の検証](ca1062.md) | 外部から参照可能なメソッドに渡されるすべての参照引数について、null かどうかをチェックする必要があります。 |
| [CA1063:IDisposable を正しく実装します](ca1063.md) | すべての IDisposable 型は、Dispose パターンを適切に実装する必要があります。 |
| [CA1064:例外は public として設定する必要があります](ca1064.md) | 内部例外は、その内部スコープ内でのみ認識されます。 内部スコープの外側にある例外は、基本例外を使用しなければキャッチできません。 内部例外が <xref:System.Exception?displayProperty=fullName>、<xref:System.SystemException?displayProperty=fullName>、または <xref:System.ApplicationException?displayProperty=fullName> を継承している場合、外部コードはその例外の処理に関する十分な情報を取得できません。 |
| [CA1065:予期しない場所に例外を発生させません](ca1065.md) | 例外をスローしないはずのメソッドが例外をスローします。 |
| [CA1066: Equals をオーバーライドする際に IEquatable を実装します](ca1066.md) | 値の型では、<xref:System.Object.Equals%2A> をオーバーライドしていますが、<xref:System.IEquatable%601>を実装していません。 |
| [CA1067: IEquatable を実装するときに Equals をオーバーライドします](ca1067.md) | 型では <xref:System.IEquatable%601> を実装していますが、<xref:System.Object.Equals%2A> メソッドをオーバーライドしていません。 |
| [CA1068:CancellationToken パラメーターは最後に指定する必要があります](ca1068.md) | メソッドに、最後のパラメーターではない CancellationToken パラメーターが指定されています。 |
| [CA1069: 列挙型には重複する値を指定できません](ca1069.md) | 列挙型に、同じ定数値が明示的に割り当てられている複数のメンバーがあります。 |
| [CA1070: イベント フィールドを virtual として宣言しません](ca1070.md) | [フィールドのように使用するイベント](../../../csharp/event-pattern.md#defining-and-raising-field-like-events)が virtual として宣言されました。 |
