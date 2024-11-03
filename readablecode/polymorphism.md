### 다형성
* 어떤 조건을 만족하면, 그 조건에 해당하는 행위를 수행한다.
* 변화 하는 것 (구체)
  * 조건 & 행위
* 변하지 않는 것 (추상)
  * 조건을 만족하는가?
  * 행위를 수행한다.
* 변하는 것과 변하지 않는 것을 분리하여 추상화하고, OCP를 지키는 구

### 숨겨져 있는 도메인 개념 도출하기
* 도메인 지식은 만드는 것이 아니라 발견하는 것
* 객체 지향은 현실을 100% 반영하는 도구가 아니라, 흉내내는 것이다.
  * 현실 세계에서 쉽게 인지하지 못하는 개념도 도출해서 사용해야 할 때가 있다.
* 설계할 때는 근시적, 거시적 관점에서 최대한 미래를 예측하고, 시간이 지나 만약 틀렸다는 것을 인지하면 언제든 돌아올 수 있도록 코드를 만들어야 한다.
  * 완벽한 설계는 없다. 그 당시의 최선이 있을 뿐.