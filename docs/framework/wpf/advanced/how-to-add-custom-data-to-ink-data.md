---
title: '방법: 잉크 데이터에 사용자 지정 데이터 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- ink data [WPF], adding custom data
- InkCanvas [WPF], displaying
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
ms.openlocfilehash: 40d883f3d3e1d504c8757c31325aa72a03da37e0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33544513"
---
# <a name="how-to-add-custom-data-to-ink-data"></a>방법: 잉크 데이터에 사용자 지정 데이터 추가
serialize 된 잉크 형식 (ISF)로 저장할 때 저장 될 잉크를 사용자 지정 데이터를 추가할 수 있습니다.  사용자 지정 데이터를 저장할 수는 <xref:System.Windows.Ink.DrawingAttributes>, <xref:System.Windows.Ink.StrokeCollection>, 또는 <xref:System.Windows.Ink.Stroke>합니다.  3 개의 개체에 사용자 지정 데이터를 저장할 수 없게 하면 데이터를 저장 하는 가장 좋은 위치를 결정할 수 있습니다.  세 클래스 모두 유사한 메서드를 사용 하 여 저장 하 고 사용자 지정 데이터에 액세스 합니다.  
  
 사용자 정의 데이터 형식만 저장할 수 있습니다.  
  
-   <xref:System.Boolean>  
  
-   <xref:System.Boolean>[]  
  
-   <xref:System.Byte>  
  
-   <xref:System.Byte>[]  
  
-   <xref:System.Char>  
  
-   <xref:System.Char>[]  
  
-   <xref:System.DateTime>  
  
-   <xref:System.DateTime>[]  
  
-   <xref:System.Decimal>  
  
-   <xref:System.Decimal>[]  
  
-   <xref:System.Double>  
  
-   <xref:System.Double>[]  
  
-   <xref:System.Int16>  
  
-   <xref:System.Int16>[]  
  
-   <xref:System.Int32>  
  
-   <xref:System.Int32>[]  
  
-   <xref:System.Int64>  
  
-   <xref:System.Int64>[]  
  
-   <xref:System.Single>  
  
-   <xref:System.Single>[]  
  
-   <xref:System.String>  
  
-   <xref:System.UInt16>  
  
-   <xref:System.UInt16>[]  
  
-   <xref:System.UInt32>  
  
-   <xref:System.UInt32>[]  
  
-   <xref:System.UInt64>  
  
-   <xref:System.UInt64>[]  
  
## <a name="example"></a>예제  
 다음 예제에서는 추가 하 고 사용자 지정 데이터를 검색 하는 <xref:System.Windows.Ink.StrokeCollection>합니다.  
  
 [!code-csharp[HowToAddCustomDataToInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 다음 예제에서는 표시 하는 응용 프로그램을 만듭니다는 <xref:System.Windows.Controls.InkCanvas> 및 두 개의 단추입니다.  단추를 `switchAuthor`, 두 개의 펜 두 명의 서로 다른 만든에서 사용할 수 있습니다.  단추 `changePenColors` 각 선의 색이 변경의 <xref:System.Windows.Controls.InkCanvas> 작성자에 따라 합니다.  두 개의 응용 프로그램 정의 <xref:System.Windows.Ink.DrawingAttributes> 각 배열에 만든 그린 나타내는 사용자 지정 속성을 추가 하 고 개체는 <xref:System.Windows.Ink.Stroke>합니다.  사용자가 클릭할 때 `changePenColors`, 응용 프로그램이 사용자 지정 속성의 값에 따라 stroke의 모양이 변경 합니다.  
  
 [!code-xaml[HowToAddCustomDataToInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]
