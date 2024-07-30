### **HTML Form 데이터 전송**

Content-Type: application/x-ww-form-urlencoded

username=kim&age=20

마치 쿼리 파라미터로 전송하지만 메시지 바디에 넣음

GET으로 하면 쿼리 파라미터로 넣음, 조회에서만 사용하자

전송 데이터를 url encoding 처리

예) abc김 -> abc%EA%B9%80

### **multipart/form-data**

파일 업로드 같은 바이너리 데이터 전송시 사용

다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart)

HTML Form 전송은 GET, POST만 지원

### **설계**

**POST**

클라이언트는 등록될 리소스의 URI를 모른다

서버가 새로 등록된 리소스 URI를 생성

컬렉션

서버가 관리하는 리소스 디렉토리

서버가 리소스의 URI를 생성하고 관리

**PUT**

클라이언트가 리소스 URI를 알고 있어야 함

클라이언트가 직접 리소스의 URI를 지정

HTML FORM 사용

GET, POST만 지원

HTTP 메서드로 해결하기 애매한 경우 컨트롤 URI 사용

**컬렉션**

예를 들어, 제가 인프런의 99번째 회원이고 유진이 님이 그 다음으로 인프런에 회원가입을 한다면

유진이님의 회원번호는 100번이 되겠죠?

이 100번이라는 숫자는 서버가 부여(할당)해주는 번호 즉 서버가 리소스(=유진이님의 100번 회원 번호를 부여하고 관리)의 URI를 결정하였다고 보면 됩니다.

**스토어**

스토어는 예를 들어, 유진이님이 인프런에 프로필 사진을 강아지.jpg라는 파일로 설정하려 할 때의 URI는

profile/강아지.jpg 가 HTTP 메소드 PUT 기반으로 등록된다고 하면

만약 프로필을 고양이 사진으로 변경하여 고양이.jpg파일을 선택하여 프로필 변경을 한다면

profile/고양이.jpg가 호출되어 파일 서버에 저장된다고 했을 때

클라이언트(=유진이님)가 리소스 URI를 결정하였다고 볼 수 있습니다.