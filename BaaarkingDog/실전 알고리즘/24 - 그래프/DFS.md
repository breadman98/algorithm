## DFS
```c++
// 인접 리스트 방식으로 저장된 그래프
// 정점은 1번~V번 까지 순차적으로 매겨져있다고 가정

<순회,비재귀>
vector<int> adj[10];
bool vis[10];

void dfs(){
  stack<int> s;
  s.push(1);
  vis[1] = true;
  
  while(!s.empty()){
    int cur= q.top(); q.pop();
    for(auto nxt : adj[cur]){
      if(vis[nxt]) continue; // 방문했으면 skip
      s.push(nxt);
      vis[nxt] = true;
    }
  }
}

<순회,재귀>
vector<int> adj[10];
bool vis[10];

void dfs(){
  vis[cur] = true;
  for(auto nxt : adj[cur]){
    if(vis[nxt]) continue; // 방문했으면 skip
    dfs(nxt);
  }
}

// 사실 비재귀와 재귀는 동작 차이가 있다.
// 재귀 : 실제 방문 할 때 방문 표시를 남김.
// 비재귀 : 방문하기 전에 아직 방문하지 않은 곳을 발견하면 그 때 방문표시를 남김.
// 일반적으로 dfs라고 한다면 재귀를 통한 동작이 맞다. 
// 비재귀는 잘 동작은 하되, 개념적으로 일치하는 동작 방식은 아님. -> 일치하게 동작 시킬 수 있긴 함(코드수정)
// 따라서 DFS만의 고유한 성질을 사용하고자 한다면 재귀를 통한 DFS를 구현하자.

<순회,비재귀2>
vector<int> adj[10];
bool vis[10];

void dfs(){
  stack<int> s;
  s.push(1);
  
  while(!s.empty()){
    int cur= q.top(); q.pop();
    if(vis[cur]) continue;
    vis[cur] = true;
    
    for(auto nxt : adj[cur]){
      if(vis[nxt]) continue; // 방문했으면 skip
      s.push(nxt);
    }
  }
}
```
