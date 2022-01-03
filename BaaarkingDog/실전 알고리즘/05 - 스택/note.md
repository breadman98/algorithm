```
스택:FILO
원소의 추가/제거 : O(1)
제일 상단의 원소 확인 : O(1)
제일 상단이 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능

스택 (stack)은 기본적인 자료구조 중 하나로, 컴퓨터 프로그램을 작성할 때 자주 이용되는 개념이다. 스택은 자료를 넣는 (push) 입구와 자료를 뽑는 (pop) 입구가 같아 제일 나중에 들어간 자료가 제일 먼저 나오는 (LIFO, Last in First out) 특성을 가지고 있다. - 출처:BOJ 1874번
```
```c++
/* 
구현

배열을 이용해서 구현해보자
필요한 것: 
원소를 담을 배열, int data[max];
인덱스를 저장할 변수 int cursor;
이 변수의 값이 곧 스택의 길이, 또는 스택 내의 원소의 수를 의미한다.
*/

#include <iostream>

using namespace std;

const int MX = 1000005;
int dat[MX];
int cursor = 0;

void push(int x){
  // cursor의 위치에 데이터를 넣고 cursor를 +1 증가시킨다.
  dat[cursor++] = x;
  //dat[cursor] = x;
  //cursor++;
}

void pop(){
  // cursor의 위치만 -1 당겨준다.
  // 어차피 나중에 push들어오면 값이 덮어써질테니
  // 삭제하는 과정을 굳이 진행하지 않아준다.
  cursor--;
}

int top(){
  // 제일 상단에 있는 데이터는
  // 현재 cursor-1 번 째에 있는 애
  return dat[cursor-1];
}

void test(){
  
  push(5);
  push(4);
  push(3);
  cout << top() << '\n'; // 3
  
  pop(); 
  pop();
  cout << top() << '\n'; // 5

  push(10); 
  push(12);
  cout << top() << '\n'; // 12

  pop();
  cout << top() << '\n'; // 10
  
}

int main() 
{
    test();
} 
```

### STL stack

<strong>추가 및 삭제</strong>
+ `push(n)`: top에 원소를 추가
+ `pop()`: top에 있는 원소를 삭제

<strong>조회</strong>
+ `top()`: top(스택의 처음이 아닌 가장 끝)에 있는 원소를 반환

<strong>기타</strong>
+ `empty()`: 스택이 비어있으면 true 아니면 false를 반환
+ `size()`: 스택 사이즈를 반환
```c++
#include <bits/stdc++.h>
using namespace std;

int main(void) {
  stack<int> S;

  S.push(10); // 10
  S.push(20); // 10 20
  S.push(30); // 10 20 30

  cout << S.size() << '\n'; // 3

  if(S.empty()) cout << "S is empty\n";
  else cout << "S is not empty\n"; // S is not empty

  S.pop(); // 10 20
  cout << S.top() << '\n'; // 20
  S.pop(); // 10
  cout << S.top() << '\n'; // 10
  S.pop(); // empty
  if(S.empty()) cout << "S is empty\n"; // S is empty
  cout << S.top() << '\n'; // stack이 비었으므로 runtime error 발생
}
```
