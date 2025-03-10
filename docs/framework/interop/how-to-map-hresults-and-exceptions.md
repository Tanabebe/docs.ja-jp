---
title: '方法: HRESULT に例外を割り当てる'
description: COM メソッドから返された HRESULT 値を .NET メソッドによってスローされる例外にマップする方法を確認します。 ランタイムは、COM と .NET の間の遷移を処理します。
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- interoperation with unmanaged code, HRESULTs
- exceptions, HRESULTs
- interoperation with unmanaged code, exceptions
- HRESULTs
- COM interop, HRESULTs
- COM interop, exceptions
ms.assetid: 610b364b-2761-429d-9c4a-afbc3e66f1b9
ms.openlocfilehash: 13798de1547428d54c10f83c41a5a402e2b3fb53
ms.sourcegitcommit: c7f0beaa2bd66ebca86362ca17d673f7e8256ca6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104872406"
---
# <a name="how-to-map-hresults-and-exceptions"></a>方法: HRESULT に例外を割り当てる

COM メソッドでは、HRESULT を返してエラーを報告します。 .NET メソッドでは、例外をスローしてエラーを報告します。 ランタイムは、この 2 つの間の遷移を処理します。 .NET Framework の例外クラスはそれぞれ HRESULT に割り当てられます。

 ユーザー定義の例外クラスは、適切な HRESULT であればどの HRESULT でも指定できます。 これらの例外クラスでは、例外オブジェクトの `HResult` フィールドを設定することで例外が生成されたときに返される HRESULT を動的に変更できます。 アンマネージ プロセスの .NET オブジェクトに実装されている `IErrorInfo` インターフェイスを通じて、クライアントに例外についての追加情報が提供されます。

 `System.Exception` を拡張するクラスを作成する場合は、構築中に HRESULT フィールドを設定する必要があります。 それ以外の場合は、基本クラスで HRESULT 値が割り当てられます。 例外のコンストラクターで値を指定することで、既存の HRESULT に新しい例外クラスを割り当てることができます。

 スレッドに `IErrorInfo` がある場合、ランタイムが `HRESULT` を無視することがあることに注意してください。  この動作は、`HRESULT` と `IErrorInfo` が同じエラーを表していない場合に発生する可能性があります。

### <a name="to-create-a-new-exception-class-and-map-it-to-an-hresult"></a>新しい例外クラスを作成し、HRESULT に割り当てるには

1. 次のコードを使用して、`NoAccessException` という新しい例外クラスを作成し、HRESULT `E_ACCESSDENIED` に割り当てます。

    ```cpp
    Class NoAccessException : public ApplicationException
    {
        NoAccessException () {
        HResult = E_ACCESSDENIED;
    }
    }
    CMyClass::MethodThatThrows
    {
    throw new NoAccessException();
    }
    ```

 マネージド コードとアンマネージド コードの両方を同時に使用する (任意のプログラミング言語の) プログラムもあります。 たとえば、次のコード例のカスタム マーシャラーは、`Marshal.ThrowExceptionForHR(int HResult)` メソッドを使用して、特定の HRESULT 値を持つ例外をスローします。 このメソッドは、HRESULT を調べ、適切な例外型を生成します。 たとえば、次のコード フラグメントの HRESULT では、`ArgumentException` が生成されます。

```cpp
CMyClass::MethodThatThrows
{
    Marshal.ThrowExceptionForHR(COR_E_ARGUMENT);
}
```

 次の表には、HRESULT から .NET の同等の例外クラスへの一般的なマッピングが示されています。 明示的なマッピングのない HRESULT 値は、`COMException` にマップされます。 完全な最新のマッピングについては、[dotnet/runtime リポジトリ](https://github.com/dotnet/runtime/blob/main/src/coreclr/vm/rexcep.h)を参照してください。

|HRESULT|.NET の例外|
|-------------|--------------------|
|`COR_E_APPLICATION`|`ApplicationException`|
|`COR_E_ARGUMENT` または `E_INVALIDARG`|`ArgumentException`|
|`COR_E_ARGUMENTOUTOFRANGE`|`ArgumentOutOfRangeException`|
|`COR_E_ARITHMETIC or ERROR_ARITHMETIC_OVERFLOW`|`ArithmeticException`|
|`COR_E_ARRAYTYPEMISMATCH`|`ArrayTypeMismatchException`|
|`COR_E_BADIMAGEFORMAT or ERROR_BAD_FORMAT`|`BadImageFormatException`|
|`COR_E_DIRECTORYNOTFOUND or ERROR_PATH_NOT_FOUND`|`DirectoryNotFoundException`|
|`COR_E_DIVIDEBYZERO`|`DivideByZeroException`|
|`COR_E_DUPLICATEWAITOBJECT`|`DuplicateWaitObjectException`|
|`COR_E_ENDOFSTREAM`|`EndOfStreamException`|
|`COR_E_ENTRYPOINTNOTFOUND`|`EntryPointNotFoundException`|
|`COR_E_EXCEPTION`|`Exception`|
|`COR_E_EXECUTIONENGINE`|`ExecutionEngineException`|
|`COR_E_FIELDACCESS`|`FieldAccessException`|
|`COR_E_FILENOTFOUND or ERROR_FILE_NOT_FOUND`|`FileNotFoundException`|
|`COR_E_FORMAT`|`FormatException`|
|`COR_E_INDEXOUTOFRANGE`|`IndexOutOfRangeException`|
|`COR_E_INVALIDCAST or E_NOINTERFACE`|`InvalidCastException`|
|`COR_E_INVALIDFILTERCRITERIA`|`InvalidFilterCriteriaException`|
|`COR_E_INVALIDOPERATION`|`InvalidOperationException`|
|`COR_E_IO`|`IOException`|
|`COR_E_MEMBERACCESS`|`AccessException`|
|`COR_E_METHODACCESS`|`MethodAccessException`|
|`COR_E_MISSINGFIELD`|`MissingFieldException`|
|`COR_E_MISSINGMANIFESTRESOURCE`|`MissingManifestResourceException`|
|`COR_E_MISSINGMEMBER`|`MissingMemberException`|
|`COR_E_MISSINGMETHOD`|`MissingMethodException`|
|`COR_E_NOTFINITENUMBER`|`NotFiniteNumberException`|
|`E_NOTIMPL`|`NotImplementedException`|
|`COR_E_NOTSUPPORTED`|`NotSupportedException`|
|`COR_E_NULLREFERENCE orE_POINTER`|`NullReferenceException`|
|`COR_E_OUTOFMEMORY or`<br /><br /> `E_OUTOFMEMORY`|`OutOfMemoryException`|
|`COR_E_OVERFLOW`|`OverflowException`|
|`COR_E_PATHTOOLONG or ERROR_FILENAME_EXCED_RANGE`|`PathTooLongException`|
|`COR_E_RANK`|`RankException`|
|`COR_E_REFLECTIONTYPELOAD`|`ReflectionTypeLoadException`|
|`COR_E_SECURITY`|`SecurityException`|
|`COR_E_SERIALIZATION`|`SerializationException`|
|`COR_E_STACKOVERFLOW orERROR_STACK_OVERFLOW`|`StackOverflowException`|
|`COR_E_SYNCHRONIZATIONLOCK`|`SynchronizationLockException`|
|`COR_E_SYSTEM`|`SystemException`|
|`COR_E_TARGET`|`TargetException`|
|`COR_E_TARGETINVOCATION`|`TargetInvocationException`|
|`COR_E_TARGETPARAMCOUNT`|`TargetParameterCountException`|
|`COR_E_THREADINTERRUPTED`|`ThreadInterruptedException`|
|`COR_E_THREADSTATE`|`ThreadStateException`|
|`COR_E_TYPELOAD`|`TypeLoadException`|
|`COR_E_TYPEINITIALIZATION`|`TypeInitializationException`|
|`COR_E_VERIFICATION`|`VerificationException`|

 拡張エラー情報を取得するために、マネージド クライアントは、生成された例外オブジェクトのフィールドを調べる必要があります。 例外オブジェクトでエラーについての有益な情報を提供できるようにするには、COM オブジェクトは、`IErrorInfo` インターフェイスを実装している必要があります。 ランタイムは、`IErrorInfo` で提供される情報を使用して例外オブジェクトを初期化します。

 COM オブジェクトで `IErrorInfo` がサポートされていない場合、ランタイムは既定値で例外オブジェクトを初期化します。 次の表で、例外オブジェクトに関連付けられた各フィールドをリストし、COM オブジェクトが `IErrorInfo` をサポートしている場合の既定の情報ソースを示します。

 スレッドに `IErrorInfo` がある場合、ランタイムが `HRESULT` を無視することがあることに注意してください。  この動作は、`HRESULT` と `IErrorInfo` が同じエラーを表していない場合に発生する可能性があります。

|例外フィールド|COM からの情報のソース|
|---------------------|------------------------------------|
|`ErrorCode`|呼び出しから返された HRESULT。|
|`HelpLink`|`IErrorInfo->HelpContext` が 0 以外の場合、文字列は `IErrorInfo->GetHelpFile`、"#"、および `IErrorInfo->GetHelpContext` を連結して形成されます。 それ以外の場合、文字列は `IErrorInfo->GetHelpFile` から返されます。|
|`InnerException`|常に null 参照 (Visual Basic では `Nothing`)。|
|`Message`|`IErrorInfo->GetDescription` から返される文字列。|
|`Source`|`IErrorInfo->GetSource` から返される文字列。|
|`StackTrace`|スタック トレース。|
|`TargetSite`|失敗を示す HRESULT を返したメソッドの名前。|

 `Message`、`Source`、および `StackTrace` などの例外フィールドは、`StackOverflowException` では使用できません。

## <a name="see-also"></a>関連項目

- [高度な COM 相互運用性](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))
- [例外](../../standard/exceptions/index.md)
