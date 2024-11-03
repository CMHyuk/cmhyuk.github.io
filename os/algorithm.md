### 페이지 교체 알고리즘
- **오프라인 알고리즘**
    - 가장 먼 미래에 참조되는 페이지와 현재의 페이지를 바꾸는 알고리즘 하지만 미래에 사용되는 프로세스를 알지 못함 -> 사용 불가
- **FIFO**
    - 가장 먼저 온 페이지부터 교제하는 방법
- **LRU**
    - 최근에 사용되지 않은 페이지를 바꾸는 방법 즉, 참조가 오래된 페이지를 바꾼다
- **NUR = NRU**
    - 일명 clock 알고리즘이라고 하며 먼저 0과 1을 가진 비트를 둔다. 1은 최근에 참조 되었고 0은 참조되지 않음을 의미 만약 한 바퀴 도는 동안 사용되지 않으면 0이 된다. 시계 방향으로 돌면서 0을 찾고 0을 찾은 순간 해당 페이지를 교체 후 1로 바꿈
- **LFU**
    - 가장 참조 횟수가 적은 페이지를 교체하는 알고리즘