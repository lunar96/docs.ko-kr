---
title: '방법: 보안 세션에 대한 보안 컨텍스트 토큰 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 640676b6-c75a-4ff7-aea4-b1a1524d71b2
ms.openlocfilehash: ec065854e049e333252003e0ce6e6efad4c6ce6c
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50193535"
---
# <a name="how-to-create-a-security-context-token-for-a-secure-session"></a>방법: 보안 세션에 대한 보안 컨텍스트 토큰 만들기
보안 세션에서 상태 저장 SCT(보안 컨텍스트 토큰)을 사용하면 세션에서 서비스 재활용의 영향을 받지 않을 수 있습니다. 예를 들어, 상태 비저장 SCT를 보안 세션에서 사용할 때 IIS(인터넷 정보 서비스)를 다시 설정하면 서비스와 연결된 세션 데이터가 손실됩니다. 이 세션 데이터에는 SCT 토큰 캐시가 포함되어 있습니다. 따라서 클라이언트가 서비스에 상태 비저장 SCT를 다음에 보낼 때 SCT와 연결된 키를 검색할 수 없기 때문에 오류가 반환됩니다. 그러나 상태 저장 SCT를 사용하는 경우에는 SCT와 연결된 키가 SCT에 포함됩니다. 키가 SCT에 포함되어 메시지에 포함되므로 서비스 재활용이 보안 세션에 영향을 주지 않습니다. 기본적으로 Windows Communication Foundation (WCF)는 보안 세션에서 상태 비저장 Sct를 사용합니다. 이 항목에서는 보안 세션에서 상태 저장 SCT를 사용하는 방법에 대해 자세히 설명합니다.  
  
> [!NOTE]
>  <xref:System.ServiceModel.Channels.IDuplexChannel>에서 파생되는 계약을 포함하는 보안 세션에서는 상태 저장 SCT를 사용할 수 없습니다.  
  
> [!NOTE]
>  보안 세션에서 상태 저장 SCT를 사용하는 응용 프로그램의 경우 서비스의 스레드 ID는 연결된 사용자 프로필이 있는 사용자 계정이어야 합니다. `Local Service`처럼 사용자 프로필이 없는 계정으로 서비스를 실행하면 예외가 throw될 수 있습니다.  
  
> [!NOTE]
>  Windows XP에서 가장이 필요한 경우 상태 저장 SCT 없이 보안 세션을 사용합니다. 상태 저장 SCT가 가장과 함께 사용되는 경우 <xref:System.InvalidOperationException>이 throw됩니다. 자세한 내용은 [지원 되지 않는 시나리오](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)합니다.  
  
### <a name="to-use-stateful-scts-in-a-secure-session"></a>보안 세션에서 상태 저장 SCT를 사용하려면  
  
-   상태 저장 SCT를 사용하는 보안 세션을 통해 SOAP 메시지를 보호하도록 지정하는 사용자 지정 바인딩을 만듭니다.  
  
    1.  추가 하 여 사용자 지정 바인딩 정의 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) 서비스 구성 파일에 있습니다.  
  
        ```xml  
        <customBinding>  
        ```  
  
    2.  추가 된 [ \<바인딩 >](../../../../docs/framework/misc/binding.md) 자식 요소를 합니다 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)합니다.  
  
         구성 파일에서 `name` 특성을 고유한 이름으로 설정하여 바인딩 이름을 지정합니다.  
  
        ```xml  
        <binding name="StatefulSCTSecureSession">  
        ```  
  
    3.  추가 하 여이 서비스에서 전송 된 메시지에 대 한 인증 모드를 지정 된 [ \<보안 >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 자식 요소를를 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)합니다.  
  
         `authenticationMode` 특성을 `SecureConversation`으로 설정하여 보안 세션을 사용하도록 지정합니다. `requireSecurityContextCancellation` 특성을 `false`로 설정하여 상태 저장 SCT를 사용하도록 지정합니다.  
  
        ```xml  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
        ```  
  
    4.  추가 하 여 보안 세션이 설정 되는 동안 클라이언트에서 인증 하는 방법을 지정는 [ \<secureConversationBootstrap >](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 자식 요소는 [ \<보안 >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)합니다.  
  
         `authenticationMode` 특성을 설정하여 클라이언트를 인증하는 방법을 지정합니다.  
  
        ```xml  
        <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        ```  
  
    5.  와 같은 인코딩 요소를 추가 하 여 메시지 인코딩을 지정 [ \<textMessageEncoding >](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md)합니다.  
  
        ```xml  
        <textMessageEncoding />  
        ```  
  
    6.  와 같은 전송 요소를 추가 하 여 전송을 지정 합니다 [ \<httpTransport >](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)합니다.  
  
        ```xml  
        <httpTransport />  
        ```  
  
     다음 코드 예제에서는 구성을 사용하여 메시지가 보안 세션에서 상태 저장 SCT와 함께 사용할 수 있는 사용자 지정 바인딩을 지정합니다.  
  
    ```xml  
    <customBinding>  
      <binding name="StatefulSCTSecureSession">  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
          <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        </security>  
        <textMessageEncoding />  
        <httpTransport />  
      </binding>  
    </customBinding>  
    ```  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate> 인증 모드를 사용하여 보안 세션을 부트스트랩하는 사용자 지정 바인딩을 만듭니다.  
  
 [!code-csharp[c_CreateStatefulSCT#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createstatefulsct/cs/secureservice.cs#2)]
 [!code-vb[c_CreateStatefulSCT#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createstatefulsct/vb/secureservice.vb#2)]  
  
 상태 저장 SCT와 함께에서 Windows 인증을 사용 하는 경우 WCF를 채우지 않습니다는 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 속성에 실제 호출자의 id 설정 되지만 대신 속성 익명입니다. WCF 보안에서는 들어오는 SCT의 모든 요청에 대해 서비스 보안 컨텍스트 내용을 다시 만들어야 합니다 때문에 서버는를 추적 하지 메모리에서 보안 세션입니다. <xref:System.Security.Principal.WindowsIdentity> 인스턴스를 SCT로 serialize할 수 없기 때문에 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 속성은 익명 ID를 반환합니다.  
  
 다음 구성에서 이 동작을 보여 줍니다.  
  
```xml  
<customBinding>  
  <binding name="Cancellation">  
       <textMessageEncoding />  
        <security   
            requireSecurityContextCancellation="false">  
              <secureConversationBootstrap />  
      </security>  
    <httpTransport />  
  </binding>  
</customBinding>  
```  
  
## <a name="see-also"></a>참고 항목  
 [\<customBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
