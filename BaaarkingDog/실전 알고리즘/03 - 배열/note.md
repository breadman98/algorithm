```
언어에서의 배열 보다는 자료구조에서의 배열이라는 것에 집중해보자
: 메모리 상에 원소를 연속하게 배치한 자료구조.
- 따라서 k번째 위치한 원소에 곧바로 접근이 가능하다(O(1)) (배열의성질1)
- 추가적으로 소모되는 메모리의 양(=overhead)가 거의 없다. (배열의성질2)
- 메모리 상에 데이터들이 붙어있어서 cache hit rate가 높다 (배열의성질3)
메모리 상에 연속한 구간을 잡아야 하기 때문에 할당에 제약이 있다 (배열의성질4)

임의의 위치에 존재하는 원소를 추가/제거 : O(N) (맨 마지막 제외)
원소를 추가/제거 함으로써 원래 있던 자리들이 밀리거나 당겨지니까
ex) a b c d e 에서 b,d사이에 A를 넣고싶다 : a b A c d e 되려면 A가 들어가고 뒤에애들 c d e 가 한 칸씩 밀림
```
```c++
#include <iostream>
using namespace std;

void insert(int idx, int num, int arr[], int& len){ 
  // len을 참조자로 받았기 때문에 원본에 영향을 줄 수 있다.
  for(int i=len; i>idx+1;i--){ // 인덱스0 번째를 생각해줘야 하기 때문에 i=len부터
    arr[i] = arr[i-1]; // 우측꺼에 좌측꺼를 넣어줌
  }
  arr[idx] = num; // 받은 idx에다가 일단 값을 넣어버린 다음에
  len++;          // 길이를 늘려줌
}

void erase(int idx, int arr[], int& len){
  for(int i=idx;i<len;i++){
    arr[i]=arr[i+1]; // 좌측꺼에 우측꺼를 넣어줌
  }
  len--;
}

void printArr(int arr[], int& len){
  for(int i = 0; i < len; i++) cout << arr[i] << ' ';
  cout << "\n\n";
}

void insert_test(){
  cout << "***** insert_test *****\n";
  int arr[10] = {10, 20, 30};
  int len = 3;
  insert(3, 40, arr, len); // 10 20 30 40
  printArr(arr, len);
  insert(1, 50, arr, len); // 10 50 20 30 40
  printArr(arr, len);
  insert(0, 15, arr, len); // 15 10 50 20 30 40
  printArr(arr, len);
}

void erase_test(){
  cout << "***** erase_test *****\n";
  int arr[10] = {10, 50, 40, 30, 70, 20};
  int len = 6;
  erase(4, arr, len); // 10 50 40 30 20
  printArr(arr, len);
  erase(1, arr, len); // 10 40 30 20
  printArr(arr, len);
  erase(3, arr, len); // 10 40 30
  printArr(arr, len);
}

int main(void) {
  insert_test();
  erase_test();
}
```
전체를 특정 값으로 초기화하는 방법들
```c++
int arr[21];
int brr[21][21];

1. memset (cstring헤더)
memset(arr,0,sizeof(arr));
memset(brr,0,sizeof(brr));
비추. 실수할 여지가 많다.
0이나 -1이 아닌 값을 넣으면 오동작
2차원 이상의 배열을 함수 인자로 넘겨 거기서 memset하면 잘못 들어간다.

2. for
for(int i=0;i<21;i++){
     arr[i] = 0;
}
for(int i=0;i<21;i++){
     for(int j=0;j<21;j++)
	brr[i][j]=0;
}

3. fill (algorithm헤더)
fill(arr,arr+21,0);
for(int i=0;i<21;i++)
     fill(brr[i],brr[i]+21,0);
```

STL vector
vector는 배열과 거의 동일한 기능을 수행하는 자료구조.
배열과 마찬가지로 원소가 메모리에 연속하게 저장되어 있다.
배열과 다른 점은 크기를 자유자재로 줄이거나 늘릴 수 있다.
```c++
int main()
{
	vector<int> v1{3,5}; // {5,5,5}
	cout<<v1.size();      // 3
	v1.push_back(7);   // {5,5,5,7}

	vector<int> v2(2);        // {0,0}
	v2.insert(v2.begin()+1,3); // {0,3,0}
	
	vector<int> v3 = {1,2,3,4}; // {1,2,3,4}
	v3.erase(v3.begin()+2);     // {1,2,4}

	vector<int> v4;   // {}
	v4 = v3	         // {1,2,4} vector에서 - 쓰면 deep-copy
	v4.pop_back();  // {1,2}. v3에는 영향x
	v4.clear();	// {}
}

원소 넣기 빼기 같은 메소드들의 시간복잡도는 O(N)임을 잘 기억하자.
```

```c
vector<int> v1 = {1,2,3,4,5};

// 1. range-based for loop ( c++11 이상 )
for(int e : v1)
     cout << e << ' ';

int e : v1 이렇게 하면 복사된 값이 e에 들어가고     
int& e : v1 이렇게 하면 원본이 e에 들어간다. 여기서 e를 바꾸면 v1의 원본이 바뀐다.


// 2. 일반적인 for loop
for(int i=0; i<v1.size(); i++)
     cout << v1[i] << ' ';

// 3. wrong
for(int i=0; i<=v1.size()-1; i++)
     cout << v1[i] << ' ';
     
vector의 size 메소드는 unsigned int를 반환하는데, 
v1이 빈 vector일 때 size가 0이라면
unsigend int 0에서 int 1을 빼는 것이 되어, unsigned int로 자동 형변환.
-1이 아니라 4294967295같은 생각치 못한 숫자가 나온다. unsigned int overflow
```

### 연습문제
```c
/*
   주어진 길이 N의 int 배열 arr에서 합이 100인 서로 다른 위치의 두 원소가
   존재하면 1을 리턴, 존재하지 않으면 0을 리턴
*/


for(int i=0; i<size; i++)
{
     if(temp[100-arr[i]]==1) 
	return 1;
     temp[arr[i]] = 1;

     return 0;
}
```
