### 사용자 수에 따른 규모 확장성
**단일 서버**
* 웹 앱, 데이터베이스, 캐시 등이 전부 서버 한 대에서 실행된다.
* 웹 서버가 다운되면 사용자는 웹 사이트에 접속할 수 없다.
* 너무 많은 사용자가 접속하면 응답 속도가 느려진다.

**로드 밸런서**
* 부하 분산 집합(load balancing set)에 속한 웹 서버들에게 부하를 트래픽을 고르게 분산하는 역할을 한다.
* 웹 서버는 클라이언트의 접속을 직접 처리하지 않는다.
  * 서버 간 통신에는 사설 IP 주소가 이용된다.

**데이터베이스 다중화**
* 서버 사이에 주(master)-부(slave) 관계를 설정하고 데이터 원본은 주 서버에, 사본은 부 서버에 저장하는 방식이다.
* 쓰기 연산은 주 데이터베이스에서만 지원, 읽기 연산은 부 데이터베이스에서만 지원한다.
* 대부분의 애플리케이션은 읽기 연산의 비중이 쓰기 연산보다 훨씬 높다.
  * 주 데이터베이스 수 < 부 데이터베이스 수
* 부 서버가 한 대 뿐인데 다운된 경우면, 읽기 연산은 한시적으로 모두 주 데이터베이스로 전달한다.
* 주 데이터베이스 서버가 다운되면, 한 대의 부 데이터베이스만 있는 경우 부 데이터베이스가 새로운 주 서버가 된다.
  * 부 서버에 보관된 데이터가 최신 상태가 아닐 수 있음
    * 복구 스크립트, 다중 마스터, 원형 다중화 방식을 도입해 해결

**캐시**
* 값비싼 연산 결과 또는 자주 참조되는 데이터를 메모리 안에 두고, 뒤이은 요청이 보다 빨리 처리될 수 있도록하는 저장소이다.
* 유의점
  * 데이터 갱신은 자주 일어나지 않지만, 참조는 빈번하게 일어나는 경우에 사용한다.
  * 캐시 서버가 재시작되면 캐시 내의 모든 데이터는 사라지기 때문에 중요 데이터는 넣지 않는다.
  * 적절한 만료시간 설정
  * 데이터 저장소의 원본과 캐시 내의 사본이 같은지에 대한 여부 
  * 단일 장애 지점(Single Point of Failure, SPOF) 가능성이 있는지
  * 캐시 메모리 크기 설정
  * 캐시가 꽉찬 경우의 데이터 방출 정책, 가장 많이 사용되는 방식은 LRU(사용된 시점이 가장 오래된 데이터), LFU(사용 빈도가 낮은 데이터)

**CDN**
* 정적 콘텐츠를 전송하는 데 쓰이는, 지리적으로 분산된 서버의 네트워크이다.
* 이미지, 비디오, CSS, JavaScript 파일 등을 캐시할 수 있다.
* 사용자가 웹 사이트를 방문하면, 그 사용자에게 가장 가까운 CDN 서버가 정적 콘텐츠를 전달한다.
* 유의점
  * CDN은 보통 제3 사업자에 의해 운영되며, 데이터 전송 양에 따라 요금을 내게 되므로 자주 사용하는 콘텐츠만 CDN을 활용하자
  * TTL이 너무 긴 경우 콘텐츠의 신선도가 떨어지고, 너무 짧은 경우 원본 서버에 빈번히 접속하므로 TTL을 적절히 설정하자
  * 만료되지 않은 콘텐츠라도 CDN에서 제거할 수 있다.
    * CDN 서비스 사업자가 제공하는 API를 이용해 콘텐츠 무효화
    * 콘텐츠의 다른 버전을 서비스하도록 오브젝트 버저닝 이용, 새로운 버전을 지정하기 위해선 URL 마지막에 버전 번호를 인자로 주면 된다.
      * ex) image.png?v=2