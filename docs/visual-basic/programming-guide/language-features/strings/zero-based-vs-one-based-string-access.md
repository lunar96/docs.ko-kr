---
title: Vs 0부터 시작 합니다. Visual Basic의 1부터 시작 하는 문자열 액세스 비교
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
ms.openlocfilehash: a0a42f72d94adf1c10865374017fa61e833df40f
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2018
ms.locfileid: "43461672"
---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a>Vs 0부터 시작 합니다. Visual Basic의 1부터 시작 하는 문자열 액세스 비교
이 항목에서는 Visual Basic 비교 및 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 문자열의 문자에 대 한 액세스를 제공 합니다. [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] Visual Basic 함수에 따라 0부터 시작 하 고 1부터 액세스를 제공 하는 반면 문자열에서 문자에 대 한 0부터 시작 액세스를 항상 제공 합니다.  
  
## <a name="one-based"></a>1부터 시작  
 1부터 Visual Basic 함수 예에 대 한 고려를 `Mid` 함수입니다. 이는 부분 문자열이 시작 되 위치 1부터 시작 문자 위치를 나타내는 인수를 사용 합니다. 합니다 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] <xref:System.String.Substring%2A?displayProperty=nameWithType> 메서드는 문자의 인덱스 부분 문자열을 시작 하려면 문자열에서 0의 위치를 사용 하 여 시작 합니다. 따라서 "ABCDE" 문자열을 해야 하는 경우 개별 문자 매겨집니다 1,2,3,4,5 사용에 대 한 합니다 `Mid` 함수를 하지만 사용 0,1,2,3,4는 <xref:System.String.Substring%2A?displayProperty=nameWithType> 메서드.  
  
## <a name="zero-based"></a>0부터 시작  
 0부터 시작 Visual Basic 함수 예에 대 한 고려를 `Split` 함수입니다. 문자열을 분할 하 고 부분 문자열이 포함 된 배열을 반환 합니다. 합니다 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] <xref:System.String.Split%2A?displayProperty=nameWithType> 메서드는 문자열을 분할 및 부분 문자열이 포함 된 배열을 반환 합니다. 때문에 합니다 `Split` 함수 및 <xref:System.String.Split%2A> 메서드가 반환 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 배열 되는 0부터 시작 합니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>  
 <xref:Microsoft.VisualBasic.Strings.Split%2A>  
 <xref:System.String.Substring%2A>  
 <xref:System.String.Split%2A>  
 [Visual Basic의 문자열 소개](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
