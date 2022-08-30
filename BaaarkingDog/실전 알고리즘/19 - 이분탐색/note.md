이분탐색 :
  - 정렬되어 있는 배열에서 특정 데이터를 찾기 위해 모든 데이터를 순차적으로 확인하는 대신 탐색 범위를 절반으로 줄여가며 찾는 탐색 방법
  
 이분탐색 주의할 점  : 
  - 주어진 배열은 반드시 정렬되어 있어야 한다.
  - mid값을 정할 때 무한 루프에 빠지지 않게 해야한다.
 ```
 start와 end를 잡아준다.
 mid = (start+end)/2 로 중간을 잡아준다.
 c++ 특성상 (start+end)가 홀수라면 나머지는 버린다.
 ```
 ## 예시
 
|||||||||||
|------|---|---|------|---|---|------|---|---|---|
|index|0|1|2|3|4|5|6|7|8|9|
|data|2|4|6|13|16|19|22|23|30|32|

 - 에서 19를 찾는다고 하면,
 - (index) start = 0, end = 9, mid = 4 
 - mid의 왼쪽에는 값이 없으니 start = mid + 1 로 변경해 범위를 절반으로 줄이고 mid를 다시 잡아준다.
 - mid = 7 
 - mid 오른쪽에 값이 없으니 end = mid - 1 로 변경해 범위를 절반으로 줄이고 mid를 다시 잡아준다.

| 찾고자 하는 값이 배열 안에 없다면 start와 end의 위치순서가 바뀌게 된다.

  - A[mid] > target : 왼쪽 구간에 대응하므로 end = mid - 1
  - A[mid] == target : 값을 찾았음
  - A[mid] < target : 오른쪽 구간에 대응하므로 start = mid + 1
  - start와 end가 역전되었다면 값을 찾지 못한 것
 
 ```c++
// 구현과 STL
 
 int a[100];
 int n;
 
 int b_search(int target)
 {
    int start = 0;
    int end = n-1;
    while(start<=end){
       int mid = (start+end)/2;
       if(a[mid]<target) start = mid + 1;
       else if(a[mid]>target) end = mid - 1;
       else return 1;
    }
    return 0; // start > end 일 경우 while문을 탈출
 }
 
 // STL binary_search 는 타겟의 존재 여부를 true/false로 반환해서 알려준다. binary_search(begin,end,target)
 ```
