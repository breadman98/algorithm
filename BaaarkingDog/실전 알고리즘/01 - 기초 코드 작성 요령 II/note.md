
### 참조(reference)
```c
C에서 swap함수
void swap(int* a, int* b)
{
     int temp = *a;
     *a = *b;
     *b = temp;	
}

C++에서 reference를 이용한 swap함수
void swap(int& a, int& b)
{
     int temp = a;
     a = b;
     b = temp;
}
```
### STL(Standard Template Library) - vector
일종의 가변배열과 비슷한 기능을 제공
```c++
vector<int> v(100);
v[20] = 10;
v[30] = 40;
```
> 일반적인 배열을 쓰듯 인덱스에 접근해서 초기화하는 모습

### STL을 함수 인자로 넘길 때
```c++
void func1(vector<int> v){
     v[10] = 7;
}
int main(){
     vector<int> v(100); // 100칸짜리 0으로 초기화된 vector v 선언
     func1(v);          
     cout << v[10];     
}
```
> 원본에 영향을 주지 않는 모습.<br>
> STL도 구조체랑 비슷하게 쌩으로 넘겨주면 복사본을 넘겨주기 때문임.
```c
bool compare(vector<int> v1, vector<int> v2, int idx){
     return v1[idx]>v2[idx];
}
```
> STL을 함수 인자로 넘겨줄 때 배열을 하나하나 복사해서 넘겨주기 때문에
> 한 번만 연산하는데 시간복잡도가 O(N)이 나와버리는 함수

참조자로 해결 가능
```c++
bool compare(vector<int>& v1, vector<int>& v2, int idx){
     return v1[idx]>v2[idx];
}
> 복사본을 만들지 않고, 참조 대상의 주소 정보만 넘어감
> 시간복잡도가 O(1)
```

### 표준 입출력
scanf()나 cin 모두 줄바꿈을 포함한 입력을 받을 때 주의해야한다.(버퍼관련)
<br>해결법들

```c++
// 1. scanf()의 옵션을 이용
char a[10];
scanf("%[^\n]",a);
```
```c++
// 2. gets 함수(보안상의 이유로 비추천)
char a[10];
gets(a);
puts(a);
```
```c++
// 3. getline 함수 사용
string s;
getline(cin,s);
cout << s;
```
### cin/cout에서 주의해야 할 점
두 명령을 실행시켜줘야 입출력으로 인한 시간초과를 방지할 수 있다.
```c++
ios::sync_with_stdio(0)
cin.tie(0)
```

printf/scanf 에서 사용하는 C stream,<br>
cout/cin 에서 사용하는 C++ stream이 분리가 되어있다.<br>
근데 이걸 섞어서 사용할 수 있게끔 동기화가 되어있는데, 동기화 때문에<br>
시간을 잡아먹을 수 있기 때문에 동기화를 끊어주겠다는 명령<br>
> ios::sync_with_stdio(false)

채점서버에서는 출력값만 따다닥 잘 나오면 정답처리 해주기 때문에<br>
굳이 버퍼에 의한 순서를 고려해줄 필요가 없다.<br>
cin 명령을 수행하기 전에 cout 버퍼를 비우지 않도록 하는 명령<br>
> cin.tie(nullptr)

#### endl 쓰지 말 것 <br>
`endl` : 개행문자를 출력하고 출력 버퍼를 비우라는 명령<br>
줄바꿈이 필요하면 endl 말고 그냥 개행문자를 출력하자.
