---
title: SignTool.exe (署名ツール)
description: SignTool.exe (署名ツール) について説明します。 このコマンド ライン ツールによって、ファイルにデジタル署名を添付し、ファイルの署名を検証し、ファイルにタイムスタンプを適用することができます。
ms.date: 03/30/2017
helpviewer_keywords:
- Sign tool
- SignTool.exe
ms.assetid: 0c25ff6c-bff3-422e-b017-146a3ee86cb9
ms.openlocfilehash: 3b4bfa70ed91f98ae49b6df3a5a29f68b30f1e0a
ms.sourcegitcommit: 1dbe25ff484a02025d5c34146e517c236f7161fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "104653856"
---
# <a name="signtoolexe-sign-tool"></a>SignTool.exe (署名ツール)

署名ツールはコマンド ライン ツールで、ファイルにデジタル署名を添付し、ファイルの署名を検証し、ファイルにタイム スタンプを付けます。  
  
 このツールは、Visual Studio と共に自動的にインストールされます。 ツールを実行するには、[、Visual Studio 開発者コマンド プロンプトまたは Visual Studio Developer PowerShell](/visualstudio/ide/reference/command-prompt-powershell) を使用します。

> [!Note]  
> Windows 10 SDK、Windows 10 HLK、Windows 10 WDK、および Windows 10 ADK **ビルド 20236 以降** の場合、ダイジェスト アルゴリズムを指定する必要があります。 SignTool の `sign` コマンドを使用するには、署名時およびタイムスタンプ時に、それぞれ `/fd` **ファイル ダイジェスト アルゴリズム** および `/td` **タイムスタンプ ダイジェスト アルゴリズム** オプションを指定する必要があります。 署名時に `/fd` が指定されていない場合、およびタイムスタンプ時に `/td` が指定されていない場合は、警告 (エラー コード 0、初期) がスローされます。 SignTool の以降のバージョンでは、警告がエラーになります。 SHA256 が推奨され、業界によって SHA1 より安全であると見なされています。  
  
 コマンド プロンプトに次のように入力します。  
  
## <a name="syntax"></a>構文  
  
```console  
signtool [command] [options] [file_name | ...]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|引数|説明|  
|--------------|-----------------|  
|`command`|4 つのコマンド (`catdb`、`sign`、`Timestamp`、または `Verify`) の 1 つで、ファイルで実行する操作を指定します。 各コマンドの詳細については、次の表を参照してください。|  
|`options`|コマンドを変更するオプションです。 グローバル オプション `/q` および `/v` のほかに、各コマンドは固有のオプション セットをサポートします。|  
|`file_name`|署名するファイルへのパスです。|  
  
 次のコマンドは、署名ツールでサポートされています。 各コマンドは、それぞれのセクションに示す個別のオプション セットと共に使用されます。  
  
|コマンド|説明|  
|-------------|-----------------|  
|`catdb`|カタログ ファイルをカタログ データベースに追加したり、カタログ データベースから削除したりします。 カタログ データベースは、カタログ ファイルの自動検索で使用され、GUID によって識別されます。 `catdb` コマンドでサポートされているオプションの一覧については、「[catdb コマンド オプション](signtool-exe.md#catdb)」を参照してください。|  
|`sign`|ファイルにデジタル署名します。 デジタル署名はファイルの改ざんを防止し、ユーザーが署名証明書に基づいて署名者を検証できるようにします。 `sign` コマンドでサポートされているオプションの一覧については、「[sign コマンド オプション](signtool-exe.md#sign)」を参照してください。|  
|`Timestamp`|ファイルにタイム スタンプを付けます。 `TimeStamp` コマンドでサポートされているオプションの一覧については、「[TimeStamp コマンド オプション](signtool-exe.md#TimeStamp)」を参照してください。|  
|`Verify`|ファイルのデジタル署名を検証します。そのために、署名証明書が信頼できる機関により発行されたかどうか、署名証明書が取り消されたかどうかを確認します。また、オプションで、署名証明書が特定のポリシーに対して有効になっているかどうかを確認します。 `Verify` コマンドでサポートされているオプションの一覧については、「[Verify コマンド オプション](signtool-exe.md#Verify)」を参照してください。|  
  
 次のオプションは、すべての署名ツール コマンドに適用されます。  
  
|Global オプション|説明|  
|-------------------|-----------------|  
|**/q**|コマンドが正常に実行した場合には何も出力されず、コマンドが失敗した場合には最小限の出力が表示されます。|  
|**/v**|コマンドが正常に実行したか、失敗したかにかかわらず、詳細出力と警告メッセージが表示されます。|  
|**/debug**|デバッグ情報を表示します。|  
  
<a name="catdb"></a>

## <a name="catdb-command-options"></a>catdb コマンド オプション  

 次の表に、`catdb` コマンドと共に使用できるオプションを示します。  
  
|Catdb オプション|説明|  
|------------------|-----------------|  
|`/d`|既定のカタログ データベースを更新するように指定します。 `/d` と `/g` のいずれのオプションも使用しない場合、署名ツールはシステム コンポーネントおよびドライバー データベースを更新します。|  
|`/g` *GUID*|グローバル一意識別子 *GUID* によって識別されるカタログ データベースを更新するように指定します。|  
|`/r`|指定したカタログをカタログ データベースから削除します。 このオプションが指定されていない場合、署名ツールはカタログ データベースに指定されたカタログを追加します。|  
|`/u`|追加されたカタログ ファイルに対して、一意な名前を自動的に生成するように指定します。 必要に応じて、既存のカタログ ファイルと名前が競合しないように、カタログ ファイルの名前が変更されます。 このオプションが指定されていない場合、署名ツールは追加されるカタログと同じ名前を持つ既存のカタログを上書きします。|  
  
<a name="sign"></a>

## <a name="sign-command-options"></a>sign コマンド オプション  

 次の表に、`sign` コマンドと共に使用できるオプションを示します。  
  
|Sign コマンド オプション|説明|  
|-------------------------|-----------------|  
|`/a`|最適な署名証明書を自動的に選択します。 署名ツールは、指定されたすべての条件を満たす有効な証明書をすべて検出し、最も長い期間有効である証明書を選択します。 このオプションが指定されていない場合、署名ツールは有効な署名証明書を 1 つだけ検索することが前提とします。|  
|`/ac`  *file*|*file* から署名ブロックに証明書を追加します。|  
|`/as`|この署名を追加します。 プライマリ署名が存在しない場合、この署名がプライマリ署名になります。|  
|`/c`  *CertTemplateName*|署名証明書に対して証明書テンプレート名 (Microsoft 拡張機能) を指定します。|  
|`/csp`  *CSPName*|秘密キー コンテナーを含む暗号化サービス プロバイダー (CSP: Cryptographic Service Provider) を指定します。|  
|`/d`  *Desc*|署名された内容の説明を指定します。|  
|`/du`  *URL*|署名された内容の詳細な説明に対する URL (Uniform Resource Locator) を指定します。|  
|`/f`  *SignCertFile*|ファイルの署名証明書を指定します。 ファイルが個人情報交換 (PFX: Personal Information Exchange) 形式でパスワードによって保護されている場合に、`/p` オプションを使用してパスワードを指定します。 ファイルに秘密キーが含まれていない場合、`/csp` および `/kc` オプションを使用して、CSP と秘密キー コンテナー名を指定します。|  
|`/fd`|ファイルの署名の作成に使用するファイル ダイジェスト アルゴリズムを指定します。 </br> **注:** 署名時に `/fd` スイッチが指定されていない場合、警告が生成されます。 既定のアルゴリズムは SHA1 ですが、SHA256 をお勧めします。|
|`/fd`  *certHash*|文字列 *certHash* を指定すると、既定でそのアルゴリズムが署名証明書に使用されるようになります。 </br> **注:** Windows 10 キット ビルド 20236 以降でのみ使用できます。|  
|`/i`  *IssuerName*|署名証明書の発行者の名前を指定します。 この値には、発行者名全体の部分文字列を指定できます。|  
|`/kc`  *PrivKeyContainerName*|秘密キー コンテナー名を指定します。|  
|`/n`  *SubjectName*|署名証明書の件名を指定します。 この値には、件名全体の部分文字列を指定できます。|  
|`/nph`|サポートされている場合に、実行可能ファイルのページ ハッシュを抑制します。 既定値は、SIGNTOOL_PAGE_HASHES 環境変数と wintrust.dll のバージョンによって決定されます。 PE ファイル以外では、このオプションは無視されます。|  
|`/p`  *Password*|PFX ファイルを開くときに使用するパスワードを指定します。 PFX ファイルを指定するには、`/f` オプションを使用します。|  
|`/p7` *パス*|指定する各コンテンツ ファイルについて公開キー暗号化規格 (PKCS) #7 ファイルを作成することを指定します。 PKCS #7 ファイルの名前は *path*\\*filename*.p7 です。|  
|`/p7ce` *Value*|署名された PKCS#7 コンテンツのオプションを指定します。 署名されたコンテンツを PKCS #7 ファイルに埋め込む場合は *Value* を "Embedded" に設定し、デタッチされた PKCS #7 ファイルの署名されたデータ部分を作成する場合には "DetachedSignedData" に設定します。 `/p7ce` オプションを使用しない場合は、既定で署名されたコンテンツが埋め込まれます。|  
|`/p7co` *\<OID>*|署名された PKCS#7 コンテンツを識別するオブジェクト識別子 (OID) を指定します。|  
|`/ph`|サポートされている場合に、実行可能ファイルのページ ハッシュを生成します。|  
|`/r`  *RootSubjectName*|署名証明書のチェーン先とするルート証明書の件名を指定します。 この値には、ルート証明書の件名全体の部分文字列を指定できます。|  
|`/s`  *StoreName*|証明書を検索するときに開くストアを指定します。 このオプションが指定されていない場合、`My` ストアが開きます。|  
|`/sha1`  *Hash*|署名証明書の SHA1 ハッシュを指定します。 以降のスイッチによって指定された条件を複数の証明書が満たす場合、一般的に SHA1 ハッシュが指定されます。|  
|`/sm`|ユーザー ストアの代わりに、コンピューター ストアを使用するように指定します。|  
|`/t`  *URL*|タイム スタンプ サーバーの URL を指定します。 このオプション (または `/tr`) が指定されていない場合、署名されたファイルにはタイム スタンプが付きません。 タイム スタンプを付けるのに失敗すると、警告が生成されます。 このオプションは、`/tr` オプションと一緒に使用することはできません。|  
|`/td`  *alg*|`/tr` オプションと共に使用して、RFC 3161 タイム スタンプ サーバーで使用されるダイジェスト アルゴリズムを要求します。 </br> **注:** タイムスタンプ時に `/td` スイッチが指定されていない場合、警告が生成されます。 既定のアルゴリズムは SHA1 ですが、SHA256 をお勧めします。 <br/> `/td` スイッチは、`/tr` スイッチの前ではなく、後で宣言する必要があります。 `/tr` スイッチの前で `/td` スイッチを宣言した場合、返されるタイムスタンプは、意図した SHA256 アルゴリズムではなく SHA1 アルゴリズムからのものになります。 |
|`/tr`  *URL*|RFC 3161 タイム スタンプ サーバーの URL を指定します。 このオプション (または `/t`) が指定されていない場合、署名されたファイルにはタイム スタンプが付きません。 タイム スタンプを付けるのに失敗すると、警告が生成されます。 このオプションは、`/t` オプションと一緒に使用することはできません。|
|`/u`  *Usage*|署名証明書に必要な拡張キー使用法 (EKU: Enhanced Key Usage) を指定します。 使用法の値は、OID または文字列によって指定できます。 既定の使用法は "Code Signing" (1.3.6.1.5.5.7.3.3) です。|  
|`/uw`|使用法 "Windows System Component Verification" (1.3.6.1.4.1.311.10.3.6) を指定します。|  
  
 使用例については、「[Using SignTool to Sign a File](/windows/desktop/SecCrypto/using-signtool-to-sign-a-file)」(SignTool を使用してファイルに署名する) を参照してください。  
  
<a name="TimeStamp"></a>

## <a name="timestamp-command-options"></a>TimeStamp コマンド オプション  

 次の表に、`TimeStamp` コマンドと共に使用できるオプションを示します。  
  
|TimeStamp オプション|説明|  
|----------------------|-----------------|  
|`/p7`|PKCS #7 ファイルにタイム スタンプを付けます。|  
|`/t`  *URL*|タイム スタンプ サーバーの URL を指定します。 タイム スタンプを付けるファイルは、事前に署名されている必要があります。 `/t` オプションまたは `/tr` オプションを指定する必要があります。|  
|`/td`  *alg*|`/tr` オプションと共に使用して、RFC 3161 タイム スタンプ サーバーで使用されるダイジェスト アルゴリズムを要求します。 </br> **注:** タイムスタンプ時に `/td` スイッチが指定されていない場合、警告が生成されます。 既定のアルゴリズムは SHA1 ですが、SHA256 をお勧めします。 <br/> `/td` スイッチは、`/tr` スイッチの前ではなく、後で宣言する必要があります。 `/tr` スイッチの前で `/td` スイッチを宣言した場合、返されるタイムスタンプは、意図した SHA256 アルゴリズムではなく SHA1 アルゴリズムからのものになります。 |
|`/tp` *index*|*index* で署名にタイム スタンプを付けます。|  
|`/tr`  *URL*|RFC 3161 タイム スタンプ サーバーの URL を指定します。 タイム スタンプを付けるファイルは、事前に署名されている必要があります。 `/tr` オプションまたは `/t` オプションを指定する必要があります。|  
  
 使用例については、「[Adding Time Stamps to Previously Signed Files](/windows/desktop/SecCrypto/adding-time-stamps-to-previously-signed-files)」(署名済みのファイルにタイム スタンプを追加する) を参照してください。  
  
<a name="Verify"></a>

## <a name="verify-command-options"></a>Verify コマンド オプション  
  
|Verify オプション|説明|  
|-------------------|-----------------|  
|`/a`|ファイルの検証にすべてのメソッドを使用できることを指定します。 まず、カタログ データベースを検索して、カタログでファイルが署名されているかどうかを確認します。 任意のカタログでファイルが署名されていない場合、署名ツールはファイルの埋め込み署名の検証を試みます。 カタログで署名されているファイルまたは署名されていないファイルを検証するときには、このオプションをお勧めします。 これらのファイルの例には、Windows ファイルまたはドライバーが含まれます。|  
|`/ad`|既定のカタログ データベースを使用してカタログを検索します。|  
|`/ag` *CatDBGUID*|*CatDBGUID* によって識別されるカタログ データベースのカタログを検索します。|  
|`/all`|複数の署名を含むファイル内のすべての署名を確認します。|  
|`/as`|システム コンポーネント (ドライバー) のカタログ データベースを使用してカタログを検索します。|  
|`/c` *CatFile*|名前でカタログ ファイルを指定します。|  
|`/d`|署名ツールで説明と説明の URL を出力するように指定します。|  
|`/ds`  *Index*|指定した位置の署名を検証します。|  
|`/hash` (`SHA1`&#124;`SHA256`)|カタログ内のファイルを検索する場合に使用するオプションのハッシュ アルゴリズムを指定します。|  
|`/kp`|カーネル モード ドライバーの署名ポリシーを使用して検証を実行するように指定します。|  
|`/ms`|複数の検証セマンティクスを使用します。 これは、Windows 8 以降での [WinVerifyTrust](/windows/desktop/api/wintrust/nf-wintrust-winverifytrust) 呼び出しの既定の動作です。|  
|`/o` *Version*|オペレーティング システムのバージョンでファイルを確認します。 *バージョン* の書式は、*PlatformID*:*VerMajor*.*VerMinor*.*BuildNumber* になります。 *PlatformID* は、<xref:System.PlatformID> 列挙メンバーの基になる値を表します。 **重要:** `/o` スイッチを使用することをお勧めします。 `/o` を指定しない場合、SignTool.exe から予期しない結果が返されることがあります。 たとえば、`/o` スイッチを含めない場合、古いオペレーティング システム上で正しく検証されるシステム カタログが新しいオペレーティング システムで正しく検証されないことがあります。|  
|`/p7`|PKCS #7 ファイルを確認します。 PKCS #7 検証で既存のポリシーは使用されません。 署名がチェックされ、署名証明書のチェーンがビルドされます。|  
|`/pa`|既定の Authenticode 検証ポリシーを使用するように指定します。 `/pa` オプションが指定されていない場合、署名ツールは Windows ドライバー検証ポリシーを使用します。 このオプションは、`catdb` オプションと一緒に使用することはできません。|  
|`/pg` *PolicyGUID*|GUID により検証ポリシーを指定します。 *PolicyGUID* は検証ポリシーの ActionID に対応しています。 このオプションは、`catdb` オプションと一緒に使用することはできません。|  
|`/ph`|署名ツールでページ ハッシュ値を出力および検証するように指定します。|  
|`/r` *RootSubjectName*|署名証明書のチェーン先とするルート証明書の件名を指定します。 この値には、ルート証明書の件名全体の部分文字列を指定できます。|  
|`/tw`|署名にタイム スタンプが付けられていない場合に、警告を生成することを指定します。|  
  
 使用例については、「[Using SignTool to Verify a File Signature](/windows/desktop/SecCrypto/using-signtool-to-verify-a-file-signature)」(SignTool を使用してファイルの署名を検証する) を参照してください。  
  
## <a name="return-value"></a>戻り値  

 署名ツールは、終了時に次のいずれかの終了コードを返します。  
  
|終了コード|説明|  
|---------------|-----------------|  
|0|実行に成功しました。|  
|1|実行に失敗しました。|  
|2|実行は完了しましたが、警告があります。|  

## <a name="examples"></a>使用例  

 カタログ ファイル MyCatalogFileName.cat をシステム コンポーネントおよびドライバー データベースに追加するコマンドを次に示します。 `/u` オプションは、必要に応じて一意の名前を生成し、`MyCatalogFileName.cat` という名前の既存のカタログ ファイルが置き換えられないようにします。  
  
```console  
signtool catdb /v /u MyCatalogFileName.cat  
```  
  
 最適な証明書を使用してファイルに自動的に署名するコマンドを次に示します。  
  
```console
signtool sign /a /fd SHA256 MyFile.exe
```

 パスワードで保護された PFX ファイルに格納されている証明書を使用してファイルにデジタル署名するコマンドを次に示します。  
  
```console  
signtool sign /f MyCert.pfx /p MyPassword /fd SHA256 MyFile.exe
```  
  
 ファイルにデジタル署名してタイム スタンプを付けるコマンドを次に示します。 ファイルへの署名に使用する証明書は、PFX ファイルに格納されています。  
  
```console  
signtool sign /f MyCert.pfx /t http://timestamp.digicert.com /fd SHA256 MyFile.exe
```  
  
 `My` ストアにある件名が `My Company Certificate` の証明書を使用してファイルに署名するコマンドを次に示します。  
  
```console  
signtool sign /n "My Company Certificate" /fd SHA256 MyFile.exe
```  
  
 ActiveX コントロールに署名して、ユーザーがコントロールをインストールするように求められるときに Internet Explorer に表示される情報を指定するコマンドを次に示します。  
  
```console  
Signtool sign /f MyCert.pfx /d: "MyControl" /du http://www.example.com/MyControl/info.html /fd SHA256 MyControl.exe
```  
  
 デジタル署名済みのファイルにタイム スタンプを付けるコマンドを次に示します。  
  
```console  
signtool timestamp /t http://timestamp.digicert.com MyFile.exe
```  

次のコマンドを使用すると、RFC 3161 タイムスタンプ サーバーを使用してファイルのタイムスタンプが設定されます。  
  
```console  
signtool timestamp /tr http://timestamp.digicert.com /td SHA256 MyFile.exe
```  
  
 ファイルが署名済みであることを検証するコマンドを次に示します。  
  
```console  
signtool verify MyFile.exe  
```  
  
 カタログで署名されている可能性があるシステム ファイルを検証するコマンドを次に示します。  
  
```console  
signtool verify /a SystemFile.dll  
```  
  
 `MyCatalog.cat` という名前のカタログで署名されているシステム ファイルを検証するコマンドを次に示します。  
  
```console  
signtool verify /c MyCatalog.cat SystemFile.dll  
```  
  
## <a name="see-also"></a>関連項目

- [ツール](index.md)
- [開発者コマンドライン シェル](/visualstudio/ide/reference/command-prompt-powershell)
