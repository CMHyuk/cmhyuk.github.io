## 네이밍
### 이름 짓기 - 단수와 복수를 구분하기
* 끝에 '-(e)s'를 붙여 어떤 데이터(변수, 클래스 등)가 단수인지, 복수인지를 나타내는 것만으로도 읽는 이에게 중요한 정보를 같이 전달할 수 있다.  

### 이름 짓기 - 이름 줄이지 않기
* 줄임말이라는 것은 가독성을 제물로 바쳐 효율성을 얻는 것으로, 대부분 잃는 것에 비해 얻는 것이 적다.
* 즉, 자제하는 것이 좋으나, 관용어 처럼 많은 사람들이 사용하는 줄임말 정도는 존재한다.
  * column -> col, latitude -> lat, longitude -> lon
  * count -> cnt (추천 x)
* 자주 사용하는 줄임말이 이해될 수 있는 것은 사실 문맥 때문

```java
class A {
    private int col; // ?
}

class TableCell {
    private int row;
    private int col; // 컬럼인가봐
}

class GeoPoint {
    private double lat;
    private double lon; // 아, 위/경도 인가보다
}
```

### 이름 짓기 - 은어/방언 사용하지 않기
* 농담에서 파생된 용어, 일부 팀원/현재의 우리 팀만 아는 용어 금지
  * 새로운 사람이 팀에 합류했을 때 이 용어를 단번에 이해할 수 있는가?
* 도메인 용어 사용하기
  * 도메인 용어를 먼저 정의하는 과정(ex 도메인 용어 사전)이 먼저 필요할 수도 있다.

### 이름 짓기 - 좋은 코드를 보고 습득하기
* 비슷한 상황에서 자주 사용하는 단어, 개념 습득하기
  * pool, candidate, threshold 등