---
title: Windows Forms의 추가 보안 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, secure calls to Windows API
- security [Windows Forms]
- security [Windows Forms], calling APIs
- Clipboard [Windows Forms], securing access
ms.assetid: 15abda8b-0527-47c7-aedb-77ab595f2bf1
ms.openlocfilehash: 0dc0ddaa1f64b75c0b4ccc1f5e73638576ea3da2
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43523484"
---
# <a name="additional-security-considerations-in-windows-forms"></a>Windows Forms의 추가 보안 고려 사항
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 보안 설정으로 인해 부분적으로 신뢰할 수 있는 환경에서는 로컬 컴퓨터에서와는 다르게 응용 프로그램이 실행될 수 있습니다. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에서는 여러 가지 중에서도 파일 시스템, 네트워크 및 관리되지 않는 API와 같은 중요한 로컬 리소스에 대한 액세스를 제한합니다. 보안 설정은 Microsoft Win32 API 또는 보안 시스템에서 확인할 수 없는 기타 API를 호출하는 기능에 영향을 줍니다. 또한 파일, 데이터 액세스, 인쇄를 비롯한 응용 프로그램의 다른 측면에도 영향을 줍니다. 부분 신뢰 환경에서의 파일 및 데이터 액세스에 대한 자세한 내용은 [Windows Forms의 파일 및 데이터 액세스 추가 보안](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)을 참조하세요. 부분 신뢰 환경에서의 인쇄에 대한 자세한 내용은 [Windows Forms의 인쇄 추가 보안](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)을 참조하세요.  
  
 다음 섹션에서는 부분 신뢰 환경에서 실행되는 응용 프로그램에서의 클립보드 사용, 창 조작 수행, Win32 API 호출 방법에 대해 설명합니다.  
  
## <a name="clipboard-access"></a>클립보드 액세스  
 합니다 <xref:System.Security.Permissions.UIPermission> 클래스를 클립보드에 연결 된 액세스 제어 <xref:System.Security.Permissions.UIPermissionClipboard> 열거형 값에 대 한 액세스 수준을 나타냅니다. 다음 표에서는 가능한 권한 수준을 보여 줍니다.  
  
|UIPermissionClipboard 값|설명|  
|---------------------------------|-----------------|  
|<xref:System.Security.Permissions.UIPermissionClipboard.AllClipboard>|클립보드 사용에 제한을 받지 않습니다.|  
|<xref:System.Security.Permissions.UIPermissionClipboard.OwnClipboard>|약간의 제한을 받으면서 클립보드를 사용할 수 있습니다. 복사 또는 잘라내기 명령 작업과 같이 클립보드에 데이터를 넣는 기능은 제한을 받지 않습니다. 텍스트 상자와 같이 붙여넣기를 허용하는 내장 컨트롤은 클립보드 데이터를 받아들일 수 있지만 사용자 정의 컨트롤은 프로그래밍 방식으로 클립보드에서 데이터를 읽을 수는 없습니다.|  
|<xref:System.Security.Permissions.UIPermissionClipboard.NoClipboard>|클립보드를 사용할 수 없습니다.|  
  
 기본적으로 로컬 인트라넷 영역 받게 <xref:System.Security.Permissions.UIPermissionClipboard.AllClipboard> 권한과 인터넷 영역 수신 <xref:System.Security.Permissions.UIPermissionClipboard.OwnClipboard> 액세스 합니다. 이것은 응용 프로그램에서 클립보드에 데이터를 복사할 수 있지만 프로그래밍 방식으로 클립보드에 데이터를 붙여넣거나 클립보드에서 데이터를 읽을 수는 없다는 것을 의미합니다. 이러한 제한으로 인해 신뢰 수준이 완전 신뢰가 아닌 프로그램은 다른 응용 프로그램이 클립보드에 복사한 내용을 읽을 수 없습니다. 응용 프로그램에 클립보드에 대한 모든 액세스가 필요하지만 해당 권한이 없을 경우에는 응용 프로그램의 권한을 높여야 합니다. 권한 높이기에 대한 자세한 내용은 [일반 보안 정책 관리](https://msdn.microsoft.com/library/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)를 참조하세요.  
  
## <a name="window-manipulation"></a>창 조작  
 합니다 <xref:System.Security.Permissions.UIPermission> 클래스 창 조작 및 기타 UI 관련 작업 및 연결 된 수행할 수 있는 권한도 제어 <xref:System.Security.Permissions.UIPermissionWindow> 열거형 값에 대 한 액세스 수준을 나타냅니다. 다음 표에서는 가능한 권한 수준을 보여 줍니다.  
  
 기본적으로 로컬 인트라넷 영역 받게 <xref:System.Security.Permissions.UIPermissionWindow.AllWindows> 권한과 인터넷 영역 수신 <xref:System.Security.Permissions.UIPermissionWindow.SafeTopLevelWindows> 액세스 합니다. 이것은 인터넷 영역에서는 응용 프로그램이 대부분의 창 작업 및 UI 작업을 수행할 수 있지만 창의 모양은 수정된다는 것을 의미합니다. 처음 실행한 경우 수정된 창에는 풍선 알림과 수정된 제목 표시줄 텍스트가 표시되며, 제목 표시줄에 닫기 단추가 필요합니다. 풍선 알림과 제목 표시줄은 응용 프로그램 사용자에게 응용 프로그램이 부분 신뢰 환경에서 실행되고 있음을 알려 줍니다.  
  
|UIPermissionWindow 값|설명|  
|------------------------------|-----------------|  
|<xref:System.Security.Permissions.UIPermissionWindow.AllWindows>|사용자는 모든 창과 사용자 입력 이벤트를 제한 없이 사용할 수 있습니다.|  
|<xref:System.Security.Permissions.UIPermissionWindow.SafeTopLevelWindows>|사용자가 안전한 최상위 창과 안전한 하위 창만 그리기 작업에 사용할 수 있고, 이러한 최상위 창 및 하위 창 내의 사용자 인터페이스에는 사용자 입력 이벤트만 사용할 수 있습니다. 이러한 안전한 창에는 명확하게 레이블이 지정되며 최소 및 최대 크기 제한이 있습니다. 제약 조건 시스템 로그온 화면이 나 시스템 바탕 화면을 모방 하는 등 잠재적으로 해로운 스푸핑 공격을 방지 및 부모 창과 포커스 관련 Api를 사용 하 여 프로그래밍 방식 액세스를 제한 합니다 <xref:System.Windows.Forms.ToolTip> 컨트롤|  
|<xref:System.Security.Permissions.UIPermissionWindow.SafeSubWindows>|사용자가 안전한 하위 창만 그리기 작업에 사용할 수 있고, 해당 하위 창 내의 사용자 인터페이스에는 사용자 입력 이벤트만 사용할 수 있습니다. 예를 들어, 브라우저 내에 표시되는 컨트롤은 안전한 하위 창입니다.|  
|<xref:System.Security.Permissions.UIPermissionWindow.NoWindows>|사용자가 창이나 사용자 인터페이스 이벤트를 사용할 수 없습니다. 사용자 인터페이스를 사용할 수 없습니다.|  
  
 각 권한 수준은 <xref:System.Security.Permissions.UIPermissionWindow> 열거형에는 해당 수준 보다 적은 수의 작업을 사용 합니다. 다음 표에서 의해 제한 되는 작업은 <xref:System.Security.Permissions.UIPermissionWindow.SafeTopLevelWindows> 및 <xref:System.Security.Permissions.UIPermissionWindow.SafeSubWindows> 값입니다. 각 멤버에 필요한 정확한 권한은 .NET Framework 클래스 라이브러리 설명서에서 해당 멤버의 항목을 참조하세요.  
  
 <xref:System.Security.Permissions.UIPermissionWindow.SafeTopLevelWindows> 사용 권한 표에 나열 된 작업을 제한 합니다.  
  
|구성 요소|제한된 작업|  
|---------------|------------------------|  
|<xref:System.Windows.Forms.Application>|-   <xref:System.Windows.Forms.Application.SafeTopLevelCaptionFormat%2A> 속성을 설정합니다.|  
|<xref:System.Windows.Forms.Control>|-시작 된 <xref:System.Windows.Forms.Control.Parent%2A> 속성입니다.<br />-   `Region` 속성을 설정합니다.<br />-호출 된 <xref:System.Windows.Forms.Control.FindForm%2A> , <xref:System.Windows.Forms.Control.Focus%2A>, <xref:System.Windows.Forms.Control.FromChildHandle%2A> 및 <xref:System.Windows.Forms.Control.FromHandle%2A>, <xref:System.Windows.Forms.Control.PreProcessMessage%2A>, <xref:System.Windows.Forms.Control.ReflectMessage%2A>, 또는 <xref:System.Windows.Forms.Control.SetTopLevel%2A> 메서드.<br />-호출 된 <xref:System.Windows.Forms.Control.GetChildAtPoint%2A> 컨트롤을 반환 하는 경우 메서드는 호출 컨트롤의 자식이 아닙니다.<br />-   컨테이너 컨트롤 내에서 컨트롤 포커스를 수정합니다.|  
|<xref:System.Windows.Forms.Cursor>|-   <xref:System.Windows.Forms.Cursor.Clip%2A> 속성을 설정합니다.<br />-호출 된 <xref:System.Windows.Forms.Control.Hide%2A> 메서드.|  
|<xref:System.Windows.Forms.DataGrid>|-호출 된 <xref:System.Windows.Forms.ContainerControl.ProcessTabKey%2A> 메서드.|  
|<xref:System.Windows.Forms.Form>|-시작 합니다 <xref:System.Windows.Forms.Form.ActiveForm%2A> 또는 <xref:System.Windows.Forms.Form.MdiParent%2A> 속성입니다.<br />-설정 된 <xref:System.Windows.Forms.Form.ControlBox%2A>, <xref:System.Windows.Forms.Form.ShowInTaskbar%2A>, 또는 <xref:System.Windows.Forms.Form.TopMost%2A> 속성입니다.<br />-설정 된 <xref:System.Windows.Forms.Form.Opacity%2A> 속성 50% 미만입니다.<br />-설정 된 <xref:System.Windows.Forms.Form.WindowState%2A> 속성을 <xref:System.Windows.Forms.FormWindowState.Minimized> 프로그래밍 방식으로 합니다.<br />-호출 된 <xref:System.Windows.Forms.Form.Activate%2A> 메서드.<br />-사용 된 <xref:System.Windows.Forms.FormBorderStyle.None>, <xref:System.Windows.Forms.FormBorderStyle.FixedToolWindow>, 및 <xref:System.Windows.Forms.FormBorderStyle.SizableToolWindow> <xref:System.Windows.Forms.FormBorderStyle> 열거형 값입니다.|  
|<xref:System.Windows.Forms.NotifyIcon>|-사용 된 <xref:System.Windows.Forms.NotifyIcon> 구성 요소를 완전히 제한 됩니다.|  
  
 합니다 <xref:System.Security.Permissions.UIPermissionWindow.SafeSubWindows> 값으로 제한 뿐만 아니라 다음 표에 나열 된 작업을 제한 합니다 <xref:System.Security.Permissions.UIPermissionWindow.SafeTopLevelWindows> 값입니다.  
  
|구성 요소|제한된 작업|  
|---------------|------------------------|  
|<xref:System.Windows.Forms.CommonDialog>|-에서 파생 된 대화 상자를 표시 합니다 <xref:System.Windows.Forms.CommonDialog> 클래스입니다.|  
|<xref:System.Windows.Forms.Control>|-호출 된 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 메서드.<br />-   <xref:System.Windows.Forms.Control.Cursor%2A> 속성을 설정합니다.|  
|<xref:System.Windows.Forms.Control.Cursor%2A>|-   <xref:System.Windows.Forms.Cursor.Current%2A> 속성을 설정합니다.|  
|<xref:System.Windows.Forms.MessageBox>|-호출 된 <xref:System.Windows.Forms.Form.Show%2A> 메서드.|  
  
### <a name="hosting-third-party-controls"></a>타사 컨트롤 호스팅  
 다른 종류의 창 조작은 양식에서 타사 컨트롤을 호스팅하는 경우에 발생할 수 있습니다. 타사 컨트롤은 사용자 지정 <xref:System.Windows.Forms.UserControl> 하지 않은 개발 하 고 직접 컴파일됩니다. 호스팅 시나리오를 악용하기는 어렵지만 타사 컨트롤이 렌더링 화면을 확장하여 사용자 양식의 전체 영역을 가리는 것이 논리적으로 가능합니다. 이 컨트롤은 중요한 대화 상자를 모방하여 사용자 이름/암호 조합이나 은행 계좌 번호 등의 정보를 사용자에게 요청할 수 있습니다.  
  
 이러한 잠재적인 위험을 방지하려면 신뢰할 수 있는 공급업체의 타사 컨트롤만 사용해야 합니다. 확인할 수 없는 소스에서 다운로드한 타사 컨트롤을 사용할 경우에는 소스 코드를 검토하여 악용 가능성이 있는지 확인하는 것이 좋습니다. 소스에 악의적인 내용이 없는지 확인한 후 어셈블리를 직접 컴파일하여 소스와 어셈블리가 일치하는지 확인해야 합니다.  
  
## <a name="win32-api-calls"></a>Win32 API 호출  
 응용 프로그램을 디자인할 때 Win32 API 함수의 호출이 필요한 경우 비관리 코드에 액세스하게 됩니다. 이 경우 Win32 API 호출이나 값을 사용할 때는 코드가 창이나 운영 체제에 대해 수행하는 작업을 확인할 수 없습니다. <xref:System.Security.Permissions.SecurityPermission> 클래스 및 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 값을 <xref:System.Security.Permissions.SecurityPermissionFlag> 열거형 비관리 코드에 액세스를 제어 합니다. 응용 프로그램 부여 된 경우에 비관리 코드에 액세스할 수는 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 권한. 기본적으로 로컬에서 실행되고 있는 응용 프로그램만 비관리 코드에 액세스할 수 있습니다.  
  
 필요한 관리 되지 않는 액세스를 제공 하는 일부 Windows Forms 멤버는 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 권한. 다음 표에서의 멤버는 <xref:System.Windows.Forms> 권한이 필요로 하는 네임 스페이스입니다. 멤버에 필요한 권한에 대한 자세한 내용은 .NET Framework 클래스 라이브러리 설명서를 참조하세요.  
  
|구성 요소|멤버|  
|---------------|------------|  
|<xref:System.Windows.Forms.Application>|-   <xref:System.Windows.Forms.Application.AddMessageFilter%2A> 메서드<br />-   <xref:System.Windows.Forms.Application.CurrentInputLanguage%2A> 속성<br />-   `Exit` 메서드<br />-   <xref:System.Windows.Forms.Application.ExitThread%2A> 메서드<br />-   <xref:System.Windows.Forms.Application.ThreadException> 이벤트|  
|<xref:System.Windows.Forms.CommonDialog>|-   <xref:System.Windows.Forms.CommonDialog.HookProc%2A> 메서드<br />-   <xref:System.Windows.Forms.CommonDialog.OwnerWndProc%2A>\ 메서드<br />-   <xref:System.Windows.Forms.CommonDialog.Reset%2A> 메서드<br />-   <xref:System.Windows.Forms.CommonDialog.RunDialog%2A> 메서드|  
|<xref:System.Windows.Forms.Control>|-   <xref:System.Windows.Forms.Control.CreateParams%2A> 메서드<br />-   <xref:System.Windows.Forms.Control.DefWndProc%2A> 메서드<br />-   <xref:System.Windows.Forms.Control.DestroyHandle%2A> 메서드<br />-   <xref:System.Windows.Forms.Control.WndProc%2A> 메서드|  
|<xref:System.Windows.Forms.Help>|-   <xref:System.Windows.Forms.Help.ShowHelp%2A> 메서드<br />-   <xref:System.Windows.Forms.Help.ShowHelpIndex%2A> 메서드|  
|<xref:System.Windows.Forms.NativeWindow>|-   <xref:System.Windows.Forms.NativeWindow> 클래스|  
|<xref:System.Windows.Forms.Screen>|-   <xref:System.Windows.Forms.Screen.FromHandle%2A> 메서드|  
|<xref:System.Windows.Forms.SendKeys>|-   <xref:System.Windows.Forms.SendKeys.Send%2A> 메서드<br />-   <xref:System.Windows.Forms.SendKeys.SendWait%2A> 메서드|  
  
 하는 경우 응용 프로그램에 비관리 코드를 호출 하는 권한을 응용 프로그램 요청 해야 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 권한 또는 하면 기능을 구현 하는 다른 방법을 고려해 야; 대부분의 경우 Windows Forms에서는 Win32 API에 대해 관리 되는 대체 함수입니다. 이러한 대안이 없는 상황에서 비관리 코드에 액세스해야 할 경우에는 응용 프로그램의 권한을 높여야 합니다.  
  
 비관리 코드를 호출할 수 있는 권한을 부여하면 응용 프로그램이 거의 모든 작업을 수행할 수 있습니다. 따라서 비관리 코드를 호출할 수 있는 권한은 신뢰할 수 있는 소스의 응용 프로그램에만 부여해야 합니다. 또는 응용 프로그램에 따라 비관리 코드를 호출하는 기능을 옵션으로 지정하거나 완전 신뢰 환경에서만 이 기능을 사용하도록 할 수 있습니다. 위험한 권한에 대한 자세한 내용은 [위험한 권한 및 정책 관리](../../../docs/framework/misc/dangerous-permissions-and-policy-administration.md)를 참조하세요. 권한 높이기에 대한 자세한 내용은 [NIB: 일반 보안 정책 관리](https://msdn.microsoft.com/library/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Windows Forms의 파일 및 데이터 액세스 추가 보안](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)  
 [Windows Forms의 인쇄 추가 보안](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)  
 [Windows Forms의 보안 개요](../../../docs/framework/winforms/security-in-windows-forms-overview.md)  
 [Windows Forms 보안](../../../docs/framework/winforms/windows-forms-security.md)  
 [ClickOnce 응용 프로그램 보안](/visualstudio/deployment/securing-clickonce-applications)
