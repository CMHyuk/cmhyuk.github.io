### **데이터 테이블 (고객 정보)**

RDB에 고객 정보가 저장된 표가 있다.

| 고객 ID | 이름 | 이메일 | 가입 날짜 |
| --- | --- | --- | --- |
| 1 | 홍길동 | hong@example.com | 2023-01-01 |
| 2 | 김철수 | kimc@example.com | 2023-02-10 |
| 3 | 이영희 | leeyh@example.com | 2023-03-15 |
| 4 | 박영수 | parkys@example.com | 2023-01-20 |

### 고객 ID 2번을 조회

---

### **B-tree 인덱스에서의 처리**

- **B-tree 인덱스**는 **고객 ID**를 기준으로 데이터를 **정렬된 트리 구조**로 저장한다. 데이터가 트리 형태로 정렬되어 있기 때문에, **이진 탐색**을 통해 고객 ID에 대한 빠른 조회가 가능하다.

### B-tree 인덱스 구조

```css

          [2]
         /   \
       [1]   [3, 4]
```

- **단계 1**: 루트 노드에서 고객 ID **2**를 찾는다.
- **단계 2**: 고객 ID **2**가 바로 루트에 존재하므로, 직접 해당 고객 정보를 반환한다.

### 조회 결과

```sql

SELECT * FROM 고객 WHERE 고객 ID = 2;
```

**결과**

| 고객 ID | 이름 | 이메일 | 가입 날짜 |
| --- | --- | --- | --- |
| 2 | 김철수 | kimc@example.com | 2023-02-10 |

### **B-tree의 장점**

- **정확한 값 조회**에서 효율적이다.
- 데이터가 **정렬된 상태**로 저장되어 있어, O(log n)의 시간 복잡도로 빠르게 조회할 수 있다.

---

### **역 인덱스에서의 처리**

- **역 인덱스**는 **문서나 텍스트 필드**에서 주로 사용되는 검색 방식으로, 각 **키워드**에 대한 인덱스를 유지한다. 하지만 이 예에서는 **ID**라는 필드도 **단어**처럼 취급되며, 고객 정보에서 **ID**를 키워드로 간주해 저장한다.

### 역 인덱스 구조 (고객 ID 기준)

| 키워드 | 고객 ID가 포함된 레코드 (문서 ID) |
| --- | --- |
| 1 | [레코드 1] |
| 2 | [레코드 2] |
| 3 | [레코드 3] |
| 4 | [레코드 4] |

- **단계 1**: 역 인덱스는 **고객 ID = 2**를 하나의 **키워드**로 인식한다.
- **단계 2**: 해당 키워드(2)가 포함된 모든 레코드를 가져온다. 여기서 바로 **레코드 2**가 반환된다.

역 인덱스에서는 **단어의 출현 여부**를 확인하는 과정이 있어, ID와 같은 **정확한 값 조회**는 추가적인 자원이 소모됩니다. **정렬된 상태**가 아니기 때문에, 해당 키워드에 대해 모든 레코드를 확인해야 한다.

### 조회 결과

| 고객 ID | 이름 | 이메일 | 가입 날짜 |
| --- | --- | --- | --- |
| 2 | 김철수 | kimc@example.com | 2023-02-10 |

### **역 인덱스의 단점**

- **정확한 값 검색**에 비효율적이다. ID를 **키워드처럼** 취급하여 검색해야 하므로, 추가적인 처리 단계가 발생하고 O(n)에 가까운 시간 복잡도가 소모될 수 있다.
- 역 인덱스는 단어 빈도와 위치를 중심으로 인덱스를 생성하는데, **정렬되지 않은 데이터**를 처리하는 데 사용된다. 이로 인해 RDB의 **정확한 값 검색**에서는 역 인덱스가 **불필요한 처리**를 요구하게 된다.

---

### **정리**

- **B-tree 인덱스**는 고객 ID와 같은 **정확한 값 검색**과 **범위 검색**에 최적화되어 있으며, 데이터가 **정렬된 상태**로 저장되므로 빠르고 효율적으로 조회할 수 있다.
- **역 인덱스**는 **텍스트 기반의 키워드 검색**에 적합하며, 고객 ID와 같은 **정확한 값**을 검색할 때는 **정렬되지 않은** 데이터 구조로 인해 성능 저하가 발생할 수 있다.