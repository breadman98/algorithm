```c++
#include <bits/stdc++.h>

using namespace std;

int n,m,ans;
string s;

int main(){
	ios::sync_with_stdio(0);
	cin.tie(0);
	
	cin>>n>>m;
	cin>>s;
	for(int i=0;i<m;i++){
		int lenIOI=0;
		if(s[i]=='I'){
			while(s[i+1]=='O'&&s[i+2]=='I'){ // IOI패턴일  계속 반복
				lenIOI++;
				if(lenIOI==n){
					ans++;
					lenIOI--; // 바로 다음 IOI칸도 검사할 수 있으므로 -1
				}
				i+=2;
			}
		}
	}
	cout<<ans;
}

```
