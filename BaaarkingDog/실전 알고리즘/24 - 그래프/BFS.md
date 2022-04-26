## BFS
```c++
// 인접 리스트 방식으로 저장된 그래프
// 정점은 1번~V번 까지 순차적으로 매겨져있다고 가정
<연결 그래프에서 순회>

vector<int> adj[10];
bool vis[10];

void bfs(){
  queue<int> q;
  q.push(1);
  vis[1] = true;
  
  while(!q.empty()){
    int cur= q.front(); q.pop();
    cout<<cur<<' ';
    for(auto nxt : adj[cur]){
      if(vis[nxt]) continue; // 방문했으면 skip
      q.push(nxt);
      vis[nxt] = true;
    }
  }
}
// 만약 인접 행렬로 구현한다?
for문을 다음과 같이 바꿈
for(int nxt=1; nxt<=V; nxt++){
  ...
  adj_matrix[cur][nxt]가 1일 때만 과정을 진행
  
}

<거리 구하는 문제>
vector<int> adj[10];
int dist[10];

void bfs(){
  fill(dist,dist+10,-1); // -1로 모두 초기화
  queue<int> q;
  q.push(1);
  dist[1] = 0; // 1번정점 거리 0으로 줌
  
  while(!q.empty()){
    int cur= q.front(); q.pop();
    for(auto nxt : adj[cur]){
      if(dist[nxt] != -1 ) continue; // 방문안했으면 skip
      q.push(nxt);
      dist[nxt] = dist[cur]+1; // 거리+1
    }
  }
}

<연결 그래프가 아닐 때 순회>
vector<int> adj[10];
bool vis[10];
int v = 9; // 정점의 수

void bfs(){
  queue<int> q;
  for(int i=1;i<=9;i++){
    if(vis[i]) continue; // for문으로 모든 정점을 간선으로 돌면서 방문했던 곳은 skip. -> 방문하지 않은 곳을 새로 찾는다.
    q.push(i);
    vis[i] = true;
  
    while(!q.empty()){
      int cur= q.front(); q.pop();
      for(auto nxt : adj[cur]){
        if(vis[nxt]) continue; // 방문했으면 skip
        q.push(nxt);
        vis[nxt] = true;
      }
    }
  }
}

```
