## Tree BFS
```c++
// 시작점을 잡으면, 그 시작점을 루트로 보낸 상황을 가정하면 편하다.
// 자신과 연결된 정점 중 1개만 부모이고, 나머지는 모두 자식이라는 성질을 이용.

// 부모 노드에 대해 자식 노드만 큐에 넣어주면 되기 때문에
// visit배열을 사용할 필요가 없어진다. 
// 그러나 visit배열을 사용하는 경우와 코드의 흐름이 다르지는 않다.

// # BFS로 Tree 순회
vector<int> adj[10];
int p[10];  // 정점의 부모 번호를 저장할 배열 p. vis배열 대신에 사용한다.
void bfs(int root)
{
  queue<int> q;
  q.push(root);
  while(!q.empty()){
    int cur = q.front(); q.pop();
    cout<<cur<<' '; // 순회하며 출력
    for(int nxt:adj[cur]){
      if(p[cur] == nxt) continue; // nxt가 부모일 경우에는 건너뛴다.
      q.push(nxt); // 부모가 아니면 큐에 넣고
      p[nxt] = cur; // 그 값을 다시 부모로 해준다.
    }
  }
}

// # depth 알아내기
vector<int> adj[10];
int p[10];
int depth[10];
voif bfs(int root)
{
  queue<int> q;
  q.push(root);
  while(!q.empty())
  {
    int cur = q.front(); q.pop();
    for(int nxt:adj[cur]){
      if(p[cur] == nxt) continue;
      q.push(nxt);
      p[nxt] = cur;
      depth[nxt] = depth[cur] + 1 ; // 자신의 depth는 부모의 depth보다 +1 인 성질을 이용함.
    }
  }
}
```
## Tree DFS
```c++
// 시작점을 잡으면, 그 시작점을 루트로 보낸 상황을 가정하면 편하다.
// 자신과 연결된 정점 중 1개만 부모이고, 나머지는 모두 자식이라는 성질을 이용.

// # DFS Tree 순회(재귀)
// 참고로 재귀 dfs는 스택 메모리가 1MB 제한이 있을 때, v가 대략 3만 이상일 때 주의할 것.
vector<int> adj[10];
int p[10];  // 정점의 부모 번호를 저장할 배열 p. vis배열 대신에 사용한다.
void dfs(int cur)
{
  cout<<cur<<' ';
  for(int nxt:adj[cur]){
    if(p[cur]==nxt) continue;
    p[nxt] = cur;
    depth[nxt] = depth[cur] + 1;
    dfs(nxt);
  }
}
```
## Binary Tree Traversal
```c++
// bfs,dfs 말고도 이진트리는 특별히
// level-order, pre-order, in-order, post-order traversal이 있다.

// 이진트리도 결국 그래프이기 때문에
// adj를 이용해서 저장을 할 수 있지만 이렇게 되면
// 왼쪽자식과 오른쪽자식 구분이 안된다.

// # 레벨 순회
int leftChild[9] = {0,2,4,6,0,0,0,0,0};
int rightChild[9] = {0,3,5,7,0,8,0,0,0};
// 노드[i]의 자식. ex) 노드3의 자식: 노드[3]의 lc=6, rc=7;
void bfs() // 
{
  queue<int> q;
  q.push(1); // root == 1
  while(!q.empty()){
    int cur = q.front(); q.pop();
    cout<<cur<<' ';
    if(leftChild[cur]) q.push(leftChild[cur]);
    if(rightChild[cur[) q.push(rightChild[cur]);
  }
}

// # 전위 순회
// # 전위 순회는 DFS와 방문 순서가 같음
int lc[9] = {0,2,4,6,0,0,0,0,0};
int rc[9] = {0,3,5,7,0,8,0,0,0};
void pre_order(int cur) // 
{
  cout<<cur<<' ';
  if(lc[cur] != 0) pre_order(lc[cur]);
  if(rc[cur] != 0) pre_order(rc[cur]);
}
// pre_order(1);

// # 중위 순회
// 만약 트리가 이진트리 였다면 자연스럽게 크기 순으로 방문하게 됨(max-heap의 경우)
int lc[9] = {0,2,4,6,0,0,0,0,0};
int rc[9] = {0,3,5,7,0,8,0,0,0};
void pre_order(int cur) // 
{
  if(lc[cur] != 0) pre_order(lc[cur]);
  cout<<cur<<' ';
  if(rc[cur] != 0) pre_order(rc[cur]);
}
// pre_order(1);

// # 후위 순회
int lc[9] = {0,2,4,6,0,0,0,0,0};
int rc[9] = {0,3,5,7,0,8,0,0,0};
void pre_order(int cur) // 
{
  if(lc[cur] != 0) pre_order(lc[cur]);
  if(rc[cur] != 0) pre_order(rc[cur]);
  cout<<cur<<' ';
}
// pre_order(1);
```
