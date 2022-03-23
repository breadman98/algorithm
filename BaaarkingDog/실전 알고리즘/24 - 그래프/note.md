
```
그래프 - 정점과 간선으로 이루어진 자료구조

정점(Vertex/Node)
간선(Edge)
차수(Degree) - 각 정점에 대해서 간선으로 연결된 이웃한 정점의 개수

```
```
# 표현법 1 - 인접행렬

정점 사이의 간선이 1개 이하인 그래프라고 할 때,
연결된 두 정점에는 1, 연결되지 않은 두 정점에는 0을 준다.
입력 예시)
5
7
31
23
41
52
54
35
24

정점개수와 간선개수 주어짐
3->1 간선
2->3 간선
이런 의미임
```
```c++
## 1. 방향 그래프
#include <iostream>

int matrix[10][10] = {};
int v,e;

int main(){
    cin>>v>>e;
    for(int i=0; i<e; i++){
        int u,v;
        cin>>u>>v;
        matrix[u][v] = 1;
    }
}

## 2. 무방향 그래프
int matrix[10][10] = {};
int v,e;

int main(){
    cin>>v>>e;
    for(int i=0; i<e; i++){
        int u,v;
        cin>>u>>v;
        matrix[u][v] = 1;
        matrix[v][u] = 1;
    }
}
```
```
# 표현법 2 - 인접 리스트

정점이 많고 간선은 상대적으로 작은 상황에서 공간을 절약할 수 있는 방식.
경우에 따라서 인접 리스트를 반드시 사용해야 하는 문제가 있다.

V개의 리스트를 만들어서 각 리스트에 자신과 연결된 정점을 저장하는 방식
편하게 STL vector를 가지고 구현
```
```c++
## 1. 방향 그래프
vector<int> adj[10];
int v,e;

int main(){
    cin>>v>>e;
    for(int i=0; i<e; i++){
      int u,v;
      cin>>u>>v;
      adj[u].push_back(v);
    }
}

## 1. 무방향 그래프
vector<int> adj[10];
int v,e;

int main(){
    cin>>v>>e;
    for(int i=0; i<e; i++){
      int u,v;
      cin>>u>>v;
      adj[u].push_back(v);
      adj[v].push_back(u);
    }
}
```
| |인접 행렬|인접 리스트|
|:---:|:---:|:---:|
|공간 복잡도|O(V^2)|O(V+E)|
|정점 u,v가 연결되어 있는지 확인하는 시간 복잡도|O(1)|O(min(deg(u),deg(v))|
|정점 v와 연결된 모든 정점을 확인하는 시간 복잡도|O(V)|O(deg(v))|
|효율적인 상황|두 점의 연결여부를 자주 확인할 때. E가 V^2에 가까울 때 |특정 정점에 연결된 모든 정점을 자주 확인할 때. E가 V^2보다 훨씬 작을 때|
