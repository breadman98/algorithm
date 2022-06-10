
## 해시

- insert, erase, find, update 의 연산이 모두 O(1)
- 충돌 회피
- 각 키의 해시 값이 최대한 균등하게 퍼져야 성능이 좋아진다. 그러기 위해서는 주어진 데이터에 대한 좋은 해시 함수를 정해야 한다. 
  1. Chaining
  2. Open addressing

### 충돌 회피 1 - Chaining
```
각 인덱스마다 연결 리스트를 둬서 충돌 회피를 하는 방법.

각 인덱스마다 연결 리스트를 하나씩 둔다. (혹은 동적배열인 vector도 상관 없음)
insert, erase, find, update 발생 시 연결 리스트로 작업을 수행한다.

STL에서 실제로 Chaining을 사용하고 있다.

Chaning은 이상적인 상황에서는 O(1)이지만
충돌이 빈번할수록 성능이 저하되고, 모든 키의 해시 값이 같은 상황(최악의상황)에서는 O(N)이 된다.
```

### 충돌 회피 2 - Open addressing
```
각 인덱스에 바로 (키,값) 쌍을 쓴다.

1. Linear Probing - 충돌 발생 시 오른쪽으로 1칸씩 이동하는 방식
장점 - 계속 인접한 배열 칸을 확인하므로 cache hit rate이 높다
단점 -Clustering이 생겨 성능에 영향을 줄 수 있다

2. Quadratic Probing - 충돌 발생 시 오른쪽으로 1,3,5... 칸씩 이동하는 방식(Linear Probing을 개선)
장점 - cache hit rate가 나쁘지 않다. Clustering을 어느 정도 회피할 수 있다
단점 - 해시 값이 같을 경우 여전히 Clustering이 발생한다

3. Dobule Hashing - 충돌 발생 시 이동할 칸의 수를 새로운 해시 함수로 계산하는 방식
(해시함수를 하나 더 둬서 충돌 발생 시 몇 칸 점프할지 계속 정함)
징점 - Clustering을 효과적으로 회피할 수 있다
단점 - cache hit rate가 낮다.
```
