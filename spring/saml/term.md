### **SAML Request**

- **정의**: SAML 요청은 서비스 SP가 IdP에게 보내는 인증 요청 메시지이다.
- **용도**: 사용자가 서비스 제공자에 접속할 때, SP는 사용자 인증을 위해 IdP로 SAML Request를 전송한다. 이 요청은 보통 리디렉션 또는 POST 방식을 통해 IdP로 전달되며, 주로 SP가 사용자를 인증해 달라는 요청을 담고 있다.

### **SAML Response**

- **정의**: SAML 응답은 IdP가 SP로 보내는 메시지로, 사용자의 인증 상태에 대한 결과를 담고 있다.
- **용도**: IdP가 사용자를 성공적으로 인증하면, SAML Response 안에 SAML Assertion을 포함하여 SP로 전달한다. SP는 이 응답을 통해 사용자가 인증되었는지 확인한다.

### **SAML Assertion**

- **정의**: SAML 어설션은 IdP가 SP에게 전달하는 **인증 정보**를 담고 있는 XML 기반의 데이터 구조이다.
- **용도**: 어설션에는 사용자의 신원 정보, 인증 여부, 인증된 시간, 권한 정보 등과 같은 데이터가 포함된다. 이 정보는 SP가 사용자의 인증 상태를 확인하는 데 사용된다.
- **구성**: 어설션은 인증, 속성, 권한을 포함할 수 있으며, 이를 통해 SP는 사용자의 다양한 속성과 권한을 확인할 수 있다.

### **XML Signatures (DSig)**

- **정의**: XML Signatures는 SAML 메시지(주로 SAML Assertion)에 디지털 서명을 추가하여 해당 메시지가 위변조되지 않았음을 보장하는 기술이다.
- **용도**: IdP는 SAML Assertion에 서명을 추가하여 SP가 해당 어설션이 신뢰할 수 있는지 확인할 수 있게 한다. SP는 IdP가 제공한 공개키를 사용해 서명을 검증한다.
- **역할**: XML Signatures는 보안성을 강화하고, 메시지의 무결성을 보장하며, 메시지가 출처로부터 변경되지 않았음을 확인한다.

### **Assertion Consumer Service (ACS)**

- **정의**: Assertion Consumer Service는 SP에서 SAML 어설션을 받아 처리하는 엔드포인트이다.
- **용도**: IdP가 인증이 완료된 후 SAML Response를 SP로 전달할 때, 그 응답은 SP의 ACS URL로 전송된다. 이 URL은 SAML 메시지를 받아 처리하고, 사용자의 인증 상태를 확인하는 곳이다.
- **예시**: SP는 여러 개의 ACS 엔드포인트를 가질 수 있으며, 각기 다른 프로토콜 바인딩(GET/POST)을 지원할 수 있다.

### **Attributes**

- **정의**: 속성(Attributes)은 SAML 어설션에 포함된 사용자의 **추가적인 정보**를 의미합니다. 이 정보는 사용자의 신원과 권한을 포함할 수 있다.
- **용도**: 예를 들어, 사용자의 이름, 이메일 주소, 역할(Role) 등이 속성으로 포함될 수 있습니다. SP는 이 속성 값을 기반으로 사용자에게 적절한 권한을 부여하거나, 시스템 내에서 특정 역할을 부여할 수 있다.

### **Relay State**

- **정의**: Relay State는 SAML 인증 과정에서 SP가 IdP로 SAML 요청을 보낼 때, 인증이 완료된 후 **돌아와야 할 경로나 상태**를 지정하는 값이다.
- **용도**: SAML 프로토콜을 사용하는 도중에 세션 상태나 리디렉션 URL을 유지하기 위해 사용됩니다. 예를 들어, 사용자가 인증 절차가 끝난 후 특정 페이지로 돌아가야 할 경우, Relay State에 해당 URL이 저장될 수 있다.
- **예시**: 사용자 A가 로그인 후 `/dashboard`로 이동해야 할 경우, 이 정보는 Relay State에 저장되어, 인증이 끝나면 해당 페이지로 이동한다.

### **SAML Trust**

- **정의**: SAML Trust는 SP와 IdP 간의 **신뢰 관계**를 의미한다.
- **용도**: SAML Trust는 SP와 IdP가 서로를 신뢰하기 위해 설정된 메커니즘을 나타낸다. 신뢰는 주로 **디지털 인증서**를 사용하여 서로의 공개키를 교환하고, 메시지의 서명을 검증하는 방식으로 이루어집니다. 이 신뢰가 설정되어야 SAML 인증 절차가 올바르게 수행될 수 있다.
- **역할**: SP는 IdP가 발급한 인증서를 신뢰하고, IdP는 SP의 요청이 신뢰할 수 있음을 보장하는 구조이다.

### **Metadata**

- **정의**: SAML 메타데이터는 SP와 IdP의 구성 정보가 포함된 **XML 문서**다.
- **용도**: SP와 IdP는 서로의 메타데이터를 공유하여, 상대방이 누구인지, 어떤 인증서를 사용하는지, 어떤 엔드포인트를 사용해야 하는지를 알 수 있습니다. 메타데이터에는 엔티티 ID, ACS URL, 서명 정보, 인증서 등이 포함된다.
- **예시**: SP는 IdP의 메타데이터를 사용해 IdP의 엔드포인트, 인증서, 프로토콜 등을 확인하고, IdP는 SP의 메타데이터를 사용해 SP와 통신할 때 필요한 정보를 얻는다.
