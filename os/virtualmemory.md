### 가상 메모리
* OS에서 사용 되는 메모리 관리 기법의 하나로 컴퓨터가 실제로 이용 가능한 메모리 자원을 추상화하여 이를 사용하는 사용자들에게 매우 큰 메모리로 보이게 만드는 것을 말한다. 
* 가상주소는 MMU와 페이지테이블에 의해 실제 주소로 변환됨 
* 페이지: 가상 메모리를 사용하는 최소 크기 단위 
* 프레임: 실제 디스크나 메모리를 사용하는 최소 크기 단위

**가상 메모리 ↔ 페이지 테이블 ↔ 램**

**페이지 테이블**
* 가상 메모리는 가상주소와 실제주소가 매핑 되어있는 페이지 테이블로 관리되며 이 때 속도 향상을 위해 캐시계층인 TLB를 사용한다. 
* 가상주소에서 바로 페이지 테이블을 가는 게 아니라 TLB에서 있는 지를 확인하고 만약 없다면 페이지 테이블로 가서 실제주소를 가져온다. 
* 가상 메모리는 작은 메모리를 매우 큰 메모리로 보이게끔 하는 것이기 때문에 참조 하려는 메모리 영역이 실제에는 없을 수도 있다. 즉, 가상 메모리에는 존재하지만 실제 메모리인 RAM에는 현재 없는 데이터나 코드에 접근할 경우가 있으며 이 때 **페이지 폴트**가 발생 
* 메모리의 당장 사용하지 않는 영역을 하드디스크로 옮기고 하드디스크의 일부분을 "마치 메모리처럼" 불러와 쓰는 것을 스와핑이라고 한다.

**페이지 폴트의 과정**
1. 참조 하려는 메모리 영역이 없음
2. 트랩 발동 운영체제 알림
3. 디스크로부터 사용하지 않는 fram을 찾음
4. 페이지 교체 알고리즘을 기반으로 스와핑
5. 해당 페이지 테이블 갱신
6. 해당 명령어를 실행

**스레싱**
* 메모리의 페이지 폴트율이 높은 것을 의미한다. 
  * 스레싱은 메모리에 너무 많은 프로세스가 동시에 올라가게 되면 스와핑이 많이 일어나서 발생 -> CPU 이용률이 낮아짐 -> 가용성을 높이기 위해 더 많은 프로세스를 메모리에 올리게 된다.