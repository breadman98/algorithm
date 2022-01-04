
```
덱:Double Ended Queue (Deque)
덱의 성질
원소의 추가/제거 O(1)
제일 앞/뒤 원소 확인 O(1)
제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능
하지만 STL deque에서는 인덱스로 원소에 접근이 가능하다.
```
```
/* 
구현

배열을 이용해서 구현해보자
필요한 것: 
원소를 담을 배열, int data[2*max+1(middle)];
앞/뒤를 가리킬 변수 int head = max, int tail = max;
덱은 앞/뒤로 원소가 삽입이 가능하기 때문에,양 옆으로 늘어날 것을
생각하여 head와 tail을 배열 사이즈의 middle로 정해준다.

*/
```
```c++
#include <iostream>

using namespace std;

const int MAX = 100005;
const int MID = MAX/2;
int dat[MAX];
int head = MID;
int tail = MID;

void push_front(int x){
  // dat[--head] = x;
  head--;
  dat[head] = x;
}

void push_back(int x){
  // dat[tail++] = x;
  dat[tail]=x;
  tail++;
}

void pop_front(){
  head++;
}
void pop_back(){
  tail--;
}

int front(){
  return dat[head];
}
int back(){
  return dat[tail-1];
}

void test(){
  push_back(30); // 30
  cout << front() << '\n'; // 30
  cout << back() << '\n'; // 30
  push_front(25); // 25 30
  push_back(12); // 25 30 12
  cout << back() << '\n'; // 12
  push_back(62); // 25 30 12 62
  pop_front(); // 30 12 62
  cout << front() << '\n'; // 30
  pop_front(); // 12 62
  cout << back() << '\n'; // 62
}

int main()
{ 
  test();
}
```
STL deque
```c++

#include <iostream>
#include <deque>
using namespace std;


int main(void){
  deque<int> DQ;

  DQ.push_front(10); // 10
  DQ.push_back(50); // 10 50
  DQ.push_front(24); // 24 10 50

  for(auto x : DQ)cout<<x<<' '; // 24 10 50
  cout << DQ.size() << '\n'; // 3
  if(DQ.empty()) cout << "DQ is empty\n";
  else cout << "DQ is not empty\n"; // DQ is not empty
  DQ.pop_front(); // 10 50
  DQ.pop_back(); // 10
  cout << DQ.back() << '\n'; // 10
  DQ.push_back(72); // 10 72
  cout << DQ.front() << '\n'; // 10
  DQ.push_back(12); // 10 72 12

  // deque에서 vector처럼 index사용해서 원소에 접근하기
  DQ[2] = 17; // 10 72 17
  DQ.insert(DQ.begin()+1, 33); // 10 33 72 17
  DQ.insert(DQ.begin()+4, 60); // 10 33 72 17 60
  for(auto x : DQ) cout << x << ' ';
  cout << '\n';
  DQ.erase(DQ.begin()+3); // 10 33 72 60
  cout << DQ[3] << '\n'; // 60
  DQ.clear(); // DQ의 모든 원소 제거
}
```

STL vector VS STL deque

|Vector|Deque|
|---|---|
|Provides insertion and deletion methods at middle and end|Provides insertion and deletion methods at middle, end, beginning|
|Bad performance for insertion and deletion at the front|Good performance for insertion and deletion at the front|
|Stores elements contiguously|It contains lists of memory chunks where elements are stored contiguously|
|Good performance for addition and deletion of elements at the end|Poor performance for addition and deletion of elements at the end|

When should we choose Deque over Vector? 
We must choose Deque when our operations are adding and deleting elements in the beginning and at the end (Double-ended queue ADT).

출처 : https://www.geeksforgeeks.org/deque-vs-vector-in-c-stl/
