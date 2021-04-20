---
description: '詳細情報: ログのストリームを取得できません'
title: ログのストリームを取得できません
ms.date: 07/20/2015
f1_keywords:
- vbrApplicationLog_ExhaustedPossibleStreamNames
ms.assetid: 33994f52-8efb-4790-a459-033e5c1db632
ms.openlocfilehash: 6eda12eb4dc2b3cf303e543a66e1f2f7d739eb6b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2021
ms.locfileid: "100455276"
---
# <a name="unable-to-obtain-a-stream-for-the-log"></a><span data-ttu-id="e8753-103">ログのストリームを取得できません</span><span class="sxs-lookup"><span data-stu-id="e8753-103">Unable to obtain a stream for the log</span></span>

<span data-ttu-id="e8753-104">ログのストリームを取得できません。</span><span class="sxs-lookup"><span data-stu-id="e8753-104">Unable to obtain a stream for the log.</span></span> <span data-ttu-id="e8753-105">\<name> に基づく、可能性のあるファイル名は既に使用されています。</span><span class="sxs-lookup"><span data-stu-id="e8753-105">Potential file names based on \<name> are already in use.</span></span>  
  
 <span data-ttu-id="e8753-106">\<name> に基づく、可能性のあるすべてのログ ファイル名が既に使用されているため、<xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> クラスは新しいログ ファイルを作成できませんでした。</span><span class="sxs-lookup"><span data-stu-id="e8753-106">The <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> class could not create a new log file because all potential log file names based on \<name> are already in use.</span></span>  
  
 <span data-ttu-id="e8753-107">ログ ファイルが多すぎる場合、アプリケーションにアーキテクチャの問題がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e8753-107">Having too many log files may indicate an architectural problem with the application.</span></span> <span data-ttu-id="e8753-108">詳細については、 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> クラスのドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e8753-108">See the documentation for the <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> class for more information.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="e8753-109">このエラーを解決するには</span><span class="sxs-lookup"><span data-stu-id="e8753-109">To correct this error</span></span>  
  
1. <span data-ttu-id="e8753-110"><xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> プロパティを <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Daily> または <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Weekly> に設定して、ログ ファイル名に日付スタンプを含めます。</span><span class="sxs-lookup"><span data-stu-id="e8753-110">Set the <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> property to <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Daily> or <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Weekly> to include a date-stamp in the log file name.</span></span>  
  
2. <span data-ttu-id="e8753-111">既存のログをアーカイブし、それらをコンピューターから削除して、 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> オブジェクトが新しいログを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e8753-111">Archive the existing logs and remove them from the computer to allow the <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> object to create new logs.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e8753-112">関連項目</span><span class="sxs-lookup"><span data-stu-id="e8753-112">See also</span></span>

- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>
- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A>
- [<span data-ttu-id="e8753-113">My.Application.Log</span><span class="sxs-lookup"><span data-stu-id="e8753-113">My.Application.Log</span></span>](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
- [<span data-ttu-id="e8753-114">My.Application.Info.DirectoryPath</span><span class="sxs-lookup"><span data-stu-id="e8753-114">My.Application.Info.DirectoryPath</span></span>](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
