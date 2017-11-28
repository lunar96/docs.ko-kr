---
title: "SaveToHistory 함수 (WPF 관리 되지 않는 API 참조)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: cpp
api_name: SaveToHistory
api_location: PresentationHost_v0400.dll
ms.assetid: 6dd101a3-44ad-4143-b228-772156f9b8ff
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: b30884433f81aa5e4bf1241ae4fe34494bef788e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2017
---
# <a name="savetohistory-function-wpf-unmanaged-api-reference"></a><span data-ttu-id="ac902-102">SaveToHistory 함수 (WPF 관리 되지 않는 API 참조)</span><span class="sxs-lookup"><span data-stu-id="ac902-102">SaveToHistory Function (WPF Unmanaged API Reference)</span></span>
<span data-ttu-id="ac902-103">이 API는 Windows Presentation Foundation (WPF) 인프라를 지원 하며 사용자 코드에서 직접 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac902-103">This API supports the Windows Presentation Foundation (WPF) infrastructure and is not intended to be used directly from your code.</span></span>  
  
 <span data-ttu-id="ac902-104">Windows 관리에 대 한 Windows Presentation Foundation (WPF) 인프라에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac902-104">Used by the Windows Presentation Foundation (WPF) infrastructure for windows management.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ac902-105">구문</span><span class="sxs-lookup"><span data-stu-id="ac902-105">Syntax</span></span>  
  
```cpp  
HRESULT SaveToHistory(  
   __in_ecount(1) IStream* pHistoryStream  
)  
```  
  
#### <a name="parameters"></a><span data-ttu-id="ac902-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac902-106">Parameters</span></span>  
 <span data-ttu-id="ac902-107">pHistoryStream</span><span class="sxs-lookup"><span data-stu-id="ac902-107">pHistoryStream</span></span>  
 <span data-ttu-id="ac902-108">기록 스트림에 대 한 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="ac902-108">A pointer to the history stream.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ac902-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ac902-109">Requirements</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ac902-110">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ac902-110">Requirements</span></span>  
 <span data-ttu-id="ac902-111">**플랫폼:** 참조 [.NET Framework 시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac902-111">**Platforms:** See [.NET Framework System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ac902-112">**DLL:**</span><span class="sxs-lookup"><span data-stu-id="ac902-112">**DLL:**</span></span>  
  
 <span data-ttu-id="ac902-113">.NET framework 3.0 및 3.5: PresentationHostDLL.dll</span><span class="sxs-lookup"><span data-stu-id="ac902-113">In the .NET Framework 3.0 and 3.5: PresentationHostDLL.dll</span></span>  
  
 <span data-ttu-id="ac902-114">.NET Framework 4 이상: PresentationHost_v0400.dll</span><span class="sxs-lookup"><span data-stu-id="ac902-114">In the .NET Framework 4 and later: PresentationHost_v0400.dll</span></span>  
  
 <span data-ttu-id="ac902-115">**.NET framework 버전:**[!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ac902-115">**.NET Framework Version:** [!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ac902-116">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ac902-116">See Also</span></span>  
 [<span data-ttu-id="ac902-117">F 관리되지 않는 API 참조</span><span class="sxs-lookup"><span data-stu-id="ac902-117">WPF Unmanaged API Reference</span></span>](../../../../docs/framework/wpf/advanced/wpf-unmanaged-api-reference.md)