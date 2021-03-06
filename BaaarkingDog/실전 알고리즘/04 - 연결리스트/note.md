### 연결리스트
```
원소들을 저장할 때 그 다음 원소가 있는 위치를 포함하는 방식으로
저장하는 자료구조
원소들은 이곳 저곳 흩어져있는데, 현재 원소가 다음원소를 기억하는 방식으로
a->b->c->...->z 이런 방식의 자료구조이다.

연결리스트의 성질
1.k번째 원소를 확인/변경하려면 O(k)가 필요함 // 배열은 O(1)
2.임의의 위치에 원소를 추가/임의 워치의 원소 제거는 O(1) // 배열은 O(N)
3.원소들이 메모리 상에 연속해있지 않아 cache hit rate가 낮지만 할당이 다소 쉽다.
```
| |배열|연결리스트|
|---|---|---|
|k번째 원소에 접근|O(1)|O(k)|
|임의 위치에 원소 확인/변경|O(1)|O(N)|
|임의 위치에 원소 추가/제거|O(N)|O(1)|
|메모리 상의 배치|연속적|불연속적|
|추가적으로 필요한 공간 (overhead)| - |O(n)|

```
연결리스트의 종류
1.단일연결리스트:각 원소가 자신의 다음 원소의 주소를 갖고있음
2.이중연결리스트:각 원소가 자신의 이전과 다음 원소의 주소를 갖고있음
3.원형연결리스트:마지막 원소가 처음 원소에 연결되어있음
```
stl에 연결리스트가 있는데, 이름은 list이고 구조는 이중연결리스트이다.

> 연결리스트의 구현
```c++
// 정석
struct NODE{
   struct NODE *prev, *next;
   int data;
}

// STL list
list<type> L
```
STL list 사용법
```c++
// STL list
int main()
{
	list<int> L = {1,2}
	list<int>::iterator t = L.begin(); // t는 1을 가리키는 중
	L.push_front(10); // 10,1,2
	cout<<*t // t가 가리키는 값 1을 출력

	L.push_back(5); // 10 1 2 5
	L.insert(t,6); // t가 가리키는 곳 앞에 6을 삽입 10 6 1 2 5
	t++; // t를 전진시킴. t가 가리키는 값은 이제 2
	t = L.erase(t); // t가 가리키는 값 제거. 그 다음 원소인 5의 위치를 반환
		       // 10 6 1 5, t가 가리키는 값은 이제 5
	
	for(list<int>::iterator i=L.begin(); i !=L.end(); i++)
		cout<< *i <<' ';

	// c++ 11이상
	for(auto i : L)
		cout<<i<<' ';
	
}

```
(이중연결리스트)

insert 
1. 새로운 원소를 생성
2. 새 원소의 prev값에 삽입할 위치의 주소를 대입
3. 새 원소의 next값에 삽입할 위치의 next값을 대입
4. 삽입할 위치의 next값과 삽입할 위치의 다음 원소의 prev값을 새 원소로 변경
 
erase
1. 이전 위치의 next를 삭제할 위치의 next로 변경
2. 다음 위치의 prev를 삭제할 위치의 prev로 변경 
3. 삭제한 애 메모리를 해제

### 연습문제 BOJ 1406
### 퀴즈
```
- 문제 1.
원형 연결 리스트 내의 임의의 노드 하나가 주어졌을 때, 해당 List의 길이를 효율적으로 구하는 방법은?

동일한 노드가 나올 때 까지 계속 다음 노드로 간다.
공간복잡도 O(1), 시간복잡도 O(N)

- 문제 2.
중간에 만나는 두 연결리스트의 시작점들이 주어졌을 때, 만나는 지점을 구하는 방법은?

두 시작점에 대해 끝까지 진행시켜서 각각의 길이를 구한다.
그 후 다시 시작점으로 돌아와서 더 긴쪽을 길이의 차이만큼 앞으로 먼저 이동시킨다.
두 시작점이 만날 때 까지 두 시작점을 동시에 한 칸씩 진행시킨다.
공간복잡도 O(1), 시간복잡도(2N)

- 문제 3.
주어진 연결 리스트 안에 사이클이 있는지 판단하라.

Floyd's cycle-finding algorithm
한 칸씩 가는 커서와 두 칸씩 가는 커서를 동일한 시작점에서 출발시킨다.
사이클이 있을 경우 두 커서는 반드시 만난다.
사이클이 없을 경우 두 커서가 만나지 못하고 연결 리스트의 끝에 도달한다.
거쳐가는 모든 노드를 저장할 필요 없는 풀이이다.
공간복잡도 O(1), 시간복잡도 O(N)
```
