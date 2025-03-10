---
title: 正規表現言語 - クイック リファレンス
description: このクイック リファレンスでは、正規表現パターンを使用して入力テキストを照合する方法について説明します。 パターンには、1 個以上の文字リテラル、演算子、またはコンストラクトが含まれます。
ms.date: 02/03/2021
ms.topic: reference
f1_keywords:
- VS.RegularExpressionBuilder
helpviewer_keywords:
- regex cheat sheet
- parsing text with regular expressions, language elements
- searching with regular expressions, language elements
- pattern-matching with regular expressions, language elements
- regular expressions, language elements
- regular expressions [.NET]
- cheat sheet
- .NET regular expressions, language elements
ms.assetid: 930653a6-95d2-4697-9d5a-52d11bb6fd4c
ms.openlocfilehash: 6228fc6fa2f21406c151378b50856ec72a6756e9
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2021
ms.locfileid: "102258919"
---
# <a name="regular-expression-language---quick-reference"></a>正規表現言語 - クイック リファレンス

正規表現とは、入力テキスト内で正規表現エンジンによる照合が試行されるパターンです。 パターンは、1 個以上の文字リテラル、演算子、または構成体で構成されます。 簡単な概要については、「[.NET の正規表現](regular-expressions.md)」を参照してください。

このクイック リファレンスの各セクションでは、正規表現の定義に使用できる特定カテゴリの文字、演算子、および構成体を一覧表示します。

また、ダウンロードして印刷し、簡単に参照できるように、この情報を 2 種類の形式で提供します。

- [Word (.docx) 形式でダウンロード](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
- [PDF (.pdf) 形式でダウンロード](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)

## <a name="character-escapes"></a>文字のエスケープ

正規表現内の円記号 (\\) は、直後の文字が特殊文字 (次の表を参照) であるか、文字どおりに解釈する必要があることを示します。 詳細については、「[文字のエスケープ](character-escapes-in-regular-expressions.md)」を参照してください。

|エスケープ文字|説明|パターン|一致件数|
|-----------------------|-----------------|-------------|-------------|
|`\a`|ビープ音文字の \u0007 と一致します。|`\a`|『`"Error!" + '\u0007'`』の「`"\u0007"`」|
|`\b`|文字クラスでバックスペースの \u0008 と一致します。|`[\b]{3,}`|『`"\b\b\b\b"`』の「`"\b\b\b\b"`」|
|`\t`|タブの \u0009 と一致します。|`(\w+)\t`|『`"item1\titem2\t"`』の「`"item1\t"`」、「`"item2\t"`」|
|`\r`|キャリッジ リターンの \u000D と一致します。 (`\r` は改行文字 `\n`とは異なります。)|`\r\n(\w+)`|『`"\r\nThese are\ntwo lines."`』の「`"\r\nThese"`」|
|`\v`|垂直タブの \u000B と一致します。|`[\v]{2,}`|『`"\v\v\v"`』の「`"\v\v\v"`」|
|`\f`|フォーム フィードの \u000C と一致します。|`[\f]{2,}`|『`"\f\f\f"`』の「`"\f\f\f"`」|
|`\n`|改行文字の \u000A と一致します。|`\r\n(\w+)`|『`"\r\nThese are\ntwo lines."`』の「`"\r\nThese"`」|
|`\e`|エスケープ文字の \u001B と一致します。|`\e`|『`"\x001B"`』の「`"\x001B"`」|
|`\` *nnn*|8 進数表現で文字を指定します (*nnn* は 2 桁または 3 桁で構成されます)。|`\w\040\w`|『`"a bc d"`』の「`"a b"`」、「`"c d"`」|
|`\x` *nn*|16 進数表現で文字を指定します (*nn* は 2 桁で構成されます)。|`\w\x20\w`|『`"a bc d"`』の「`"a b"`」、「`"c d"`」|
|`\c` *X*<br /><br /> `\c` *x*|*X* または *x* で指定された ASCII の制御文字と一致します。 *X* または *x* は制御文字です。|`\cC`|『`"\x0003"`』(Ctrl-C) の「`"\x0003"`」|
|`\u` *nnnn*|16 進数形式で表される Unicode 文字 ( *nnnn* で表される 4 桁の数字) と一致します。|`\w\u0020\w`|『`"a bc d"`』の「`"a b"`」、「`"c d"`」|
|`\`|このトピック内の表に示されているエスケープ文字として認識されない文字が後ろに付いている場合は、その文字と一致します。 たとえば、`\*` は `\x2A`と同じであり、`\.` は `\x2E`と同じです。 これを使用すると、正規表現エンジンによって言語要素 (\* や ? など) と文字リテラル (`\*` や `\?` など) のあいまいさが解消されます。|`\d+[\+-x\*]\d+`|『`"(2+2) * 3*9"`』の「`"2+2"`」と「`"3*9"`」|

## <a name="character-classes"></a>文字クラス

文字クラスは、文字セットのいずれかと一致します。 文字クラスに含まれる言語要素を次の表に示します。 詳細については、「 [文字クラス](character-classes-in-regular-expressions.md)」を参照してください。

|文字クラス|説明|パターン|一致件数|
|---------------------|-----------------|-------------|-------------|
|`[` *character_group* `]`|*character_group* 内の任意の 1 文字と一致します。 既定では、大文字と小文字が区別されます。|`[ae]`|『`"gray"`』の「`"a"`」<br /><br /> 『`"lane"`』の「`"a"`」、「`"e"`」|
|`[^` *character_group* `]`|否定:*character_group* 内にない任意の 1 文字と一致します。 既定では、*character_group* の文字について、大文字と小文字が区別されます。|`[^aei]`|『`"reign"`』の「`"r"`」、「`"g"`」、「`"n"`」|
|`[` *first* `-` *last* `]`|文字範囲:*first* から *last* までの範囲にある任意の 1 文字と一致します。|`[A-Z]`|『`"AB123"`』の「`"A"`」、「`"B"`」|
|`.`|ワイルドカード:\n を除く任意の 1 文字と一致します。<br /><br /> リテラルのピリオド文字 (. または `\u002E`) と一致させるには、この文字の前にエスケープ文字 (`\.`) を指定します。|`a.e`|『`"nave"`』の「`"ave"`」<br /><br /> 『`"water"`』の「`"ate"`」|
|`\p{` *name* `}`|*name* で指定された名前付きブロックまたは Unicode 一般カテゴリ内の任意の 1 文字と一致します。|`\p{Lu}`<br /><br /> `\p{IsCyrillic}`|『`"City Lights"`』の「`"C"`」、「`"L"`」<br /><br /> 『`"ДЖem"`』の「`"Д"`」、「`"Ж"`」|
|`\P{` *name* `}`|*name* で指定された名前付きブロックまたは Unicode 一般カテゴリにない任意の 1 文字と一致します。|`\P{Lu}`<br /><br /> `\P{IsCyrillic}`|『`"City"`』の「`"i"`」、「`"t"`」、「`"y"`」<br /><br /> 『`"ДЖem"`』の「`"e"`」、「`"m"`」|
|`\w`|単語に使用される任意の文字と一致します。|`\w`|『`"ID A1.3"`』の「`"I"`」、「`"D"`」、「`"A"`」、「`"1"`」、「`"3"`」|
|`\W`|単語に使用される文字以外の任意の文字と一致します。|`\W`|『`"ID A1.3"`』の「`" "`」、「`"."`」|
|`\s`|空白文字と一致します。|`\w\s`|『`"ID A1.3"`』の「`"D "`」|
|`\S`|空白以外の文字と一致します。|`\s\S`|『`"int __ctr"`』の「`" _"`」|
|`\d`|10 進数字と一致します。|`\d`|『`"4 = IV"`』の「`"4"`」|
|`\D`|10 進数以外の任意の文字と一致します。|`\D`|『`"4 = IV"`』の「`" "`」、「`"="`」、「`" "`」、「`"I"`」、「`"V"`」|

## <a name="anchors"></a>アンカー

アンカー (アトミック ゼロ幅アサーション) を使用すると、文字列内での現在位置によって一致するかどうかが決まります。しかし、エンジンで後方の文字列が読み込まれたり、複数の文字と一致したりすることはありません。 アンカーであるメタ文字を次の表に示します。 詳細については、「 [アンカー](anchors-in-regular-expressions.md)」を参照してください。

|アサーション|説明|パターン|一致件数|
|---------------|-----------------|-------------|-------------|
|`^`|既定では、文字列の先頭で一致する必要があります。複数行モードでは、行の先頭で一致する必要があります。|`^\d{3}`|『`"901-333-"`』の「`"901"`」|
|`$`|既定では、文字列の末尾で一致するか、文字列の末尾にある `\n` の前で一致する必要があります。複数行モードでは、行の末尾の前で一致するか、行の末尾にある `\n` の前で一致する必要があります。|`-\d{3}$`|『`"-901-333"`』の「`"-333"`」|
|`\A`|文字列の先頭で一致する必要があります。|`\A\d{3}`|『`"901-333-"`』の「`"901"`」|
|`\Z`|文字列の末尾で一致するか、文字列の末尾にある `\n` の前で一致する必要があります。|`-\d{3}\Z`|『`"-901-333"`』の「`"-333"`」|
|`\z`|文字列の末尾で一致する必要があります。|`-\d{3}\z`|『`"-901-333"`』の「`"-333"`」|
|`\G`|前回の一致が終了した位置で一致する必要があります。|`\G\(\d\)`|『`"(1)(3)(5)[7](9)"`』の「`"(1)"`」、「`"(3)"`」、「`"(5)"`」|
|`\b`|`\w` (英数字) と `\W` (英数字以外) 文字の境界位置で一致する必要があります。|`\b\w+\s\w+\b`|『`"them theme them them"`』の「`"them theme"`」、「`"them them"`」|
|`\B`|`\b` 境界以外で一致する必要があります。|`\Bend\w*\b`|『`"end sends endure lender"`』の「`"ends"`」、「`"ender"`」|

## <a name="grouping-constructs"></a>グループ化構成体

グループ化構成体は、正規表現の部分式を表し、通常は入力文字列の部分文字列をキャプチャします。 グループ化構成体に含まれる言語要素を次の表に示します。 詳細については、「 [グループ化構成体](grouping-constructs-in-regular-expressions.md)」を参照してください。

|グループ化構成体|説明|パターン|一致件数|
|------------------------|-----------------|-------------|-------------|
|`(` *subexpression* `)`|一致した部分式をキャプチャして、1 から始まる序数を代入します。|`(\w)\1`|『`"deep"`』の「`"ee"`」|
|`(?<` *name* `>` *subexpression* `)`<br /> or <br />`(?'` *name* `'` *subexpression* `)`|一致した部分式を名前付きグループにキャプチャします。|`(?<double>\w)\k<double>`|『`"deep"`』の「`"ee"`」|
|`(?<` *name1* `-` *name2* `>` *subexpression* `)` <br /> or <br /> `(?'` *name1* `-` *name2* `'` *subexpression* `)`|グループ定義の均等化を定義します。 詳細については、「 [グループ化構成体](grouping-constructs-in-regular-expressions.md)」の「グループ定義の均等化」を参照してください。|`(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$`|『`"3+2^((1-3)*(3-1))"`』の「`"((1-3)*(3-1))"`」|
|`(?:` *subexpression* `)`|非キャプチャ グループを定義します。|`Write(?:Line)?`|『`"Console.WriteLine()"`』の「`"WriteLine"`」<br /><br /> 『`"Console.Write(value)"`』の「`"Write"`」|
|`(?imnsx-imnsx:` *subexpression* `)`|指定したオプションを *subexpression* に適用するか、または無効にします。 詳細については、「 [正規表現のオプション](regular-expression-options.md)」を参照してください。|`A\d{2}(?i:\w+)\b`|『`"A12xl A12XL a12xl"`』の「`"A12xl"`」、「`"A12XL"`」|
|`(?=` *subexpression* `)`|ゼロ幅の肯定先読みアサーションです。|`\b\w+\b(?=.+and.+)`|`"cats"`, `"dogs"`<br/>in<br/>`"cats, dogs and some mice."`|
|`(?!` *subexpression* `)`|ゼロ幅の否定先読みアサーションです。|`\b\w+\b(?!.+and.+)`|`"and"`, `"some"`, `"mice"`<br/>in<br/>`"cats, dogs and some mice."`|
|`(?<=` *subexpression* `)`|ゼロ幅の正の後読みアサーションです。|`\b\w+\b(?<=.+and.+)`<br/><br/>&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;<br/><br/>`\b\w+\b(?<=.+and.*)`|`"some"`, `"mice"`<br/>in<br/>`"cats, dogs and some mice."`<br/>&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;<br/>`"and"`, `"some"`, `"mice"`<br/>in<br/>`"cats, dogs and some mice."`|
|`(?<!` *subexpression* `)`|ゼロ幅の負の後読みアサーションです。|`\b\w+\b(?<!.+and.+)`<br/><br/>&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;<br/><br/>`\b\w+\b(?<!.+and.*)`|`"cats"`, `"dogs"`, `"and"`<br/>in<br/>`"cats, dogs and some mice."`<br/>&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;&mdash;<br/>`"cats"`, `"dogs"`<br/>in<br/>`"cats, dogs and some mice."`|
|`(?>` *subexpression* `)`|アトミック グループ。|`(?>a\|ab)c`|`"ac"` の `"ac"`<br/><br/>`"abc"` には "_なし_"|

### <a name="lookarounds-at-a-glance"></a>Lookaround の概要

正規表現エンジンは、**lookaround 式** にヒットすると、現在位置から元の文字列の開始 (後読み) または終了 (先読み) に達する部分文字列を取得し、lookaround パターンを使用してその部分文字列で <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> を実行します。 この部分式の結果の成功は、それが肯定または否定のどちらのアサーションであるかによって決まります。

| Lookaround | 名前 | 機能 |
| - | - | - |
`(?=check)` | 肯定先読み | 文字列内の現在位置の直後にあるものが "check" であることをアサートします
`(?<=check)` | 肯定後読み | 文字列内の現在位置の直前にあるものが "check" であることをアサートします
`(?!check)` | 否定先読み  | 文字列内の現在位置の直後にあるものが "check" ではないことをアサートします
`(?<!check)` | 否定後読み | 文字列内の現在位置の直前にあるものが "check" ではないことをアサートします

一致すると、パターンの残りの部分で一致によるエラーが発生しても、**アトミック グループ** は再評価されません。 これにより、アトミック グループ内またはパターンの残りの部分で量指定子が発生した場合に、パフォーマンスを大幅に向上させることができます。

## <a name="quantifiers"></a>量指定子

量指定子は、一致するために、入力文字列中に直前の要素 (文字、グループ、または文字クラス) がいくつ存在しなければならないかを指定します。 量指定子に含まれる言語要素を次の表に示します。 詳細については、「 [量指定子](quantifiers-in-regular-expressions.md)」を参照してください。

|量指定子|説明|パターン|一致件数|
|----------------|-----------------|-------------|-------------|
|`*`|直前の要素と 0 回以上一致します。|`\d*\.\d`|`".0"`, `"19.9"`, `"219.9"`|
|`+`|直前の要素と 1 回以上一致します。|`"be+"`|『`"been"`』の「`"bee"`」、『`"bent"`』の「`"be"`」|
|`?`|直前の要素と 0 回または 1 回一致します。|`"rai?n"`|`"ran"`, `"rain"`|
|`{` *n* `}`|直前の要素とちょうど *n* 回一致します。|`",\d{3}"`|『`"1,043.6"`』の「`",043"`」、『`"9,876,543,210"`』の「`",876"`」、「`",543"`」、および「`",210"`」|
|`{` *n* `,}`|直前の要素と *n* 回以上一致します。|`"\d{2,}"`|`"166"`, `"29"`, `"1930"`|
|`{` *n* `,` *m* `}`|直前の要素と *n* 回以上 *m* 回以下で一致します。|`"\d{3,5}"`|`"166"`, `"17668"`<br /><br /> 『`"193024"`』の「`"19302"`」|
|`*?`|直前の要素と 0 回以上 (ただし、できるだけ少ない回数) 一致します。|`\d*?\.\d`|`".0"`, `"19.9"`, `"219.9"`|
|`+?`|直前の要素と 1 回以上 (ただし、できるだけ少ない回数) 一致します。|`"be+?"`|『`"been"`』の「`"be"`」、『`"bent"`』の「`"be"`」|
|`??`|直前の要素と 0 回または 1 回 (ただし、できるだけ少ない回数) 一致します。|`"rai??n"`|`"ran"`, `"rain"`|
|`{` *n* `}?`|直前の要素とちょうど *n* 回一致します。|`",\d{3}?"`|『`"1,043.6"`』の「`",043"`」、『`"9,876,543,210"`』の「`",876"`」、「`",543"`」、および「`",210"`」|
|`{` *n* `,}?`|直前の要素と *n* 回以上 (ただし、できるだけ少ない回数) 一致します。|`"\d{2,}?"`|`"166"`, `"29"`, `"1930"`|
|`{` *n* `,` *m* `}?`|直前の要素と *n* 回以上 *m* 回以下 (ただし、できるだけ少ない回数) 一致します。|`"\d{3,5}?"`|`"166"`, `"17668"`<br /><br /> 『`"193024"`』の「`"193"`」、「`"024"`」|

## <a name="backreference-constructs"></a>前方参照構成体

前方参照を使用すると、以前に一致した部分式を、同じ正規表現内で引き続き識別できます。 .NET の正規表現でサポートされている前方参照構成体を、次の表に示します。 詳細については、「 [前方参照構成体](backreference-constructs-in-regular-expressions.md)」を参照してください。

|前方参照構成体|説明|パターン|一致件数|
|-----------------------------|-----------------|-------------|-------------|
|`\` *number*|前方参照。 番号付き部分式の値に一致します。|`(\w)\1`|『`"seek"`』の「`"ee"`」|
|`\k<` *name* `>`|名前付き前方参照。 名前付きの式の値に一致します。|`(?<char>\w)\k<char>`|『`"seek"`』の「`"ee"`」|

## <a name="alternation-constructs"></a>代替構成体

代替構成体は、OR 一致を有効にするように正規表現を変更します。 これらの構成体に含まれる言語要素を次の表に示します。 詳細については、「 [代替構成体](alternation-constructs-in-regular-expressions.md)」を参照してください。

|代替構成体|説明|パターン|一致件数|
|---------------------------|-----------------|-------------|-------------|
|<code>&#124;</code>|縦棒 (<code>&#124;</code>) 文字で区切られたいずれかの要素と一致します。|<code>th(e&#124;is&#124;at)</code>|『`"this is the day."`』の「`"the"`」、「`"this"`」|
|`(?(` *expression* `)` *yes* <code>&#124;</code> *no* `)`|*expression* で指定される正規表現パターンが一致する場合は *yes* と一致します。それ以外の場合は、*no* (省略可能) 部分と一致します。 *expression* はゼロ幅アサーションとして解釈されます。|<code>(?(A)A\d{2}\b&#124;\b\d{3}\b)</code>|『`"A10 C103 910"`』の「`"A10"`」、「`"910"`」|
|`(?(` *name* `)` *yes* <code>&#124;</code> *no* `)`|名前付きまたは番号付きのキャプチャ グループ *name* に一致が見つかった場合は *yes* と一致します。それ以外の場合は *no*(省略可能) と一致します。|<code>(?&lt;quoted&gt;&quot;)?(?(quoted).+?&quot;&#124;\S+\s)</code>|『`"Dogs.jpg \"Yiska playing.jpg\""`』の「`"Dogs.jpg "`」、「`"\"Yiska playing.jpg\""`」|

## <a name="substitutions"></a>置換

置換は、置換パターンでサポートされる正規表現言語要素です。 詳細については、「 [置換](substitutions-in-regular-expressions.md)」を参照してください。 アトミック ゼロ幅アサーションであるメタ文字を次の表に示します。

|文字|説明|パターン|置換パターン|入力文字列|結果文字列|
|---------------|-----------------|-------------|-------------------------|------------------|-------------------|
|`$` *number*|グループの *number* と一致した部分文字列に置換されます。|`\b(\w+)(\s)(\w+)\b`|`$3$2$1`|`"one two"`|`"two one"`|
|`${` *name* `}`|名前付きグループの *name* と一致した部分文字列に置換されます。|`\b(?<word1>\w+)(\s)(?<word2>\w+)\b`|`${word2} ${word1}`|`"one two"`|`"two one"`|
|`$$`|"$" リテラルに置換されます。|`\b(\d+)\s?USD`|`$$$1`|`"103 USD"`|`"$103"`|
|`$&`|一致したパターン全体と同じパターンに置換されます。|`\$?\d*\.?\d+`|`**$&**`|`"$1.30"`|`"**$1.30**"`|
|``$` ``|一致した場所より前にある入力文字列のすべてに置換されます。|`B+`|``$` ``|`"AABBCC"`|`"AAAACC"`|
|`$'`|一致した場所より後にある入力文字列のすべてに置換されます。|`B+`|`$'`|`"AABBCC"`|`"AACCCC"`|
|`$+`|キャプチャされた最後のグループに置換されます。|`B+(C+)`|`$+`|`"AABBCCDD"`|`"AACCDD"`|
|`$_`|入力文字列全体に置換されます。|`B+`|`$_`|`"AABBCC"`|`"AAAABBCCCC"`|

## <a name="regular-expression-options"></a>正規表現のオプション

正規表現エンジンで正規表現パターンを解釈する方法を制御するオプションを指定できます。 これらのオプションの多くは、インラインで (正規表現パターンで) 指定することも、1 つ以上の <xref:System.Text.RegularExpressions.RegexOptions> 定数として指定することもできます。 このクイック リファレンスでは、インライン オプションのみを示しています。 インライン オプションと <xref:System.Text.RegularExpressions.RegexOptions> オプションの詳細については、「 [正規表現のオプション](regular-expression-options.md)」を参照してください。

インライン オプションは、次の 2 種類の方法で指定できます。

- [その他の構成体](miscellaneous-constructs-in-regular-expressions.md) `(?imnsx-imnsx)`の使用。オプションまたはオプション セットの前に負符号 (-) がある場合、そのオプションが無効になります。 たとえば、`(?i-mn)` では、大文字と小文字を区別しない一致 (`i`) がオン、複数行モード (`m`) がオフ、名前のないグループ キャプチャ (`n`) がオフになります。 このオプションは、このオプションが定義されている位置から正規表現パターンに適用され、パターンの末尾まで、または別の構成体によってオプションが反転する位置まで有効になります。
- [グループ化構造体](grouping-constructs-in-regular-expressions.md)`(?imnsx-imnsx:`*subexpression*`)` を使用する。これは、指定されたグループのみに対してオプションを定義します。

.NET の正規表現エンジンでは、次のインライン オプションがサポートされます。

|オプション|説明|パターン|一致件数|
|------------|-----------------|-------------|-------------|
|`i`|大文字と小文字を区別しない一致を使用します。|`\b(?i)a(?-i)a\w+\b`|『`"aardvark AAAuto aaaAuto Adam breakfast"`』の「`"aardvark"`」、「`"aaaAuto"`」|
|`m`|複数行モードを使用します。 `^` と `$` は、(入力文字列の先頭および末尾ではなく) 各行の先頭および末尾と一致します。|例については、「 [正規表現のオプション](regular-expression-options.md)」の「複数行モード」を参照してください。||
|`n`|名前のないグループをキャプチャしません。|例については、「 [正規表現のオプション](regular-expression-options.md)」の「明示的なキャプチャのみ」を参照してください。||
|`s`|単一行モードを使用します。|例については、「 [正規表現のオプション](regular-expression-options.md)」の「単一行モード」を参照してください。||
|`x`|正規表現パターンでエスケープされていない空白を無視します。|`\b(?x) \d+ \s \w+`|『`"1 aardvark 2 cats IV centurions"`』の「`"1 aardvark"`」、「`"2 cats"`」|

## <a name="miscellaneous-constructs"></a>その他の構成体

その他の構成体は、正規表現パターンを変更するか、それに関する情報を指定します。 次の表に .NET でサポートされているその他の構成体を示します。 詳細については、「 [その他の構成体](miscellaneous-constructs-in-regular-expressions.md)」を参照してください。

|構成体|定義|例|
|---------------|----------------|-------------|
|`(?imnsx-imnsx)`|パターンの途中で、大文字と小文字の区別などのオプションを設定または無効化します。詳細については、「[正規表現のオプション](regular-expression-options.md)」を参照してください。|「`\bA(?i)b\w+\b`」は『`"ABA Able Act"`』の「`"ABA"`」、「`"Able"`」と一致する|
|`(?#` *comment* `)`|インライン コメントです。 コメントは、最初の閉じかっこで終了します。|`\bA(?#Matches words starting with A)\w+\b`|
|`#` [to end of line]|X モード コメントです。 コメントの先頭はエスケープされない `#` で、コメントは行末まで継続します。|`(?x)\bA\w+\b#Matches words starting with A`|

## <a name="see-also"></a>関連項目

- <xref:System.Text.RegularExpressions?displayProperty=nameWithType>
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- [正規表現](regular-expressions.md)
- [正規表現クラス](the-regular-expression-object-model.md)
- [正規表現 - クイック リファレンス (Word 形式でダウンロード)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
- [正規表現 - クイック リファレンス (PDF 形式でダウンロード)](https://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)
