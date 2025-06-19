# 复制字符串
补全：
```
int main()
{
    char s1[256], s2[256];
    int n, pos;
    cin >> n;
    cin.get();
    cin.getline(s1, n+1);
    cin >> pos;
    strcpypos(s2, s1, pos);
    cout << s2 << endl;
    return 0;
}
```
只写函数部分：
```cpp
void strcpypos(string s2,string s1,int pos){

    s1->s2;
    int i=0;
    while(s1[pos-1+i]!='\0'){
        s2[i]=s1[pos-1+i];
    }
   s2[i]='\0';
}
```
记得加\0就行。

# 不等长字符串排序
```cpp
int main()
{
    void sort(char *[], int n);
    int i;
    char str[10][80];
    char *p[10];
    int n;
    cin >> n;
    for (i= 0; i < n; i++)
        cin>>str[i];
    for (i= 0; i < n; i++)
        p[i]= str[i];
    sort(p, n);
    for (i= 0; i < n; i++)
        cout << p[i] << endl;
    return 0;
}
```
只写sort部分
```
void sort(char *str[], int n){
    char *t;
    for(int i=0;i<n-1;i++){
        for(int j=0;j<n-i-1;j++){
            if (strcmp(str[j], str[j + 1]) > 0){
                t=str[j];
                str[j]=str[j+1];
                str[j+1]=t;
            }
        }
    }

}
```
注意点：

* 冒泡排序
* strcmp函数
* 传参*str[]; 
#  01 串排序

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

// 比较函数：按长度、1的数量、字典序排序
bool compare(const string& a, const string& b) {
    if (a.size() != b.size()) return a.size() < b.size();

    int aOnes = count(a.begin(), a.end(), '1');
    int bOnes = count(b.begin(), b.end(), '1');
    if (aOnes != bOnes) return aOnes < bOnes;

    return a < b;  // 默认字典序
}

int main() {
    vector<string> arr;
    string s;

    // 读取全部输入（支持多行）
    while (getline(cin, s)) {
        if (!s.empty())
            arr.push_back(s);
    }

    // 使用自定义的 compare 函数排序
    sort(arr.begin(), arr.end(), compare);

    // 输出排序结果
    for (const auto& str : arr) {
        cout << str << '\n';
    }

    return 0;
}
```
* 自定义函数排序。
* 字符串数组：输入方式；输出方式；
* count函数int aOnes = count(a.begin(), a.end(), '1');
 # 折半查找关键字
 ```
#include<bits/stdc++.h>
using namespace std;
struct nums{
    int num;
    int se;
};
vector<nums> number;
 int n;
bool cmp(nums x,nums y){
    return x.num<y.num;
}
void binary(int target){
    int left=0;
    int right=n-1;
    bool a=false;
    while(left<=right){
        int mid=(left+right)/2;
        if(target==number[mid].num){
            a=true;
            cout<<mid+1<<" "<<number[mid].se<<endl;
            break;
        }
        else if(target>number[mid].num){
            left=mid+1;
           
        }
        else {
            right=mid-1;
            
        }
    }
    if(!a){
        cout<<"-1"<<endl;
    }

}
int main(){

    cin>>n;
    number=vector<nums> (n);
 
    for(int i=0;i<n;i++){
        cin>>number[i].num;
        number[i].se=i+1;
    }
    int t;
    cin>>t;
    vector<int> sea(t);
    sort(number.begin(),number.end(),cmp);
    for(int i=0;i<t;i++){
       cin>>sea[i];
      
       binary(sea[i]);
    }
return 0;
}
```
# 鹊桥相会
说那么麻烦，结果是找最快的那一只。
```
#include <iostream>
#include <vector>
#include <cmath>
#include <limits>
using namespace std;

int main() {
    int w,n;//宽度，只数
    int pos,v;
    cin>>w>>n;
    int it,it_min,in=0;
    w=w*1000;
    for(int i=0;i<n;i++){
        cin>>pos>>v;
        if(pos<=0&&v>0){
           it=(w-pos)/v;
           in++;
        }
        if(it_min>it||in==1){
            it_min=it;
        }
    }
    if(in)
    cout<<it_min<<endl;
    else cout<<"can't"<<endl;
    return 0;
}
```
# 聪明的矿工
**二维前缀和**
```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

int main() {
    int n;
    cin>>n;
    vector<vector<int>> row_sum(n+1,vector<int>(n+1,0));
    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++){
            int num;
            cin>>num;
            row_sum[i][j]=row_sum[i][j-1]+num;
        }
    }
    
    int maxsum=-1e9;
    for(int left=0;left<n;left++){
        for(int right=left+1;right<=n;right++){
            int sumrow=0;
            for(int row=1;row<=n;row++){

                int sum=row_sum[row][right]-row_sum[row][left];
                sumrow=max(sum,sumrow+sum);
                maxsum=max(maxsum,sumrow);
            }
        }
    }
    cout<<maxsum<<endl;
    return 0;
}
```
# 共享单车
```
#include<bits/stdc++.h>
using namespace std;

int dx[]={-1,1,0,0,-1,1,-1,1};
int dy[]={0,0,-1,1,-1,-1,1,1};
int distance1[]={100,100,100,100,141,141,141,141};
int n,m,t;
vector<vector<char>> map1;
//vector<vector<bool>> visi;

struct Node{
    int x,y;
    int dis;
};

int bfs(int sx, int sy){
    vector<vector<int>> distan(n,vector<int>(m,1e9));
    //visi.resize(n,vector<bool>(m, false));
    int shortway=1e9;
    queue <Node> q;
    q.push({sx, sy,0});
    //visi[sx][sy]=true;
    distan[sx][sy] =0;

    while(!q.empty()){
        Node current=q.front();
        q.pop();
         if(current.dis>distan[current.x][current.y])
         continue;
        if(map1[current.x][current.y]=='x'){
            shortway=min(shortway,current.dis);
        }

        for(int i=0; i<8;i++){
            int nx=current.x+ dx[i];
            int ny=current.y +dy[i];
            int nd=current.dis+distance1[i];
          
            if(nx>= 0&&nx<n&&ny>=0&&ny<m&& map1[nx][ny] != '*'){
                if(nd<distan[nx][ny])
                {distan[nx][ny] = nd;
               // cout<<distan[nx][ny]<<endl;
               //visi[nx][ny] = true;
                q.push({nx, ny,nd});}
            }
        }
    }

    return shortway;
}

int main(){
    cin >> t;
    while(t--){
        cin >> n >> m;
        map1.resize(n, vector<char>(m));
        int a, b;
        for(int i = 0; i < n;i++){
            for(int j = 0; j<m; j++){
                cin>>map1[i][j];
                if(map1[i][j]=='o'){
                    a=i; b=j;
                }
            }
        }
        int result = bfs(a,b);    
            
        if(result!=1e9) cout <<result<<endl;
        else cout<<-1<<endl;
        
    }
    return 0;
}
```
这个个一定要多看几遍，只有distance数组来记录最小路径，当前距离比已经记录的小的时候再入队列，用shortway记录最短距离。
# N皇后
简单的回溯
```cpp
#include <iostream>
#include <vector>
#include<queue>
using namespace std;
int n;
vector<vector<int>> chessboard;

bool isvalid(int row,int col){
     for(int i=0;i<row;i++){
        if(chessboard[i][col]==1)
        return false;
     }
     for(int i=row-1,j=col+1;i>=0&&j<n;i--,j++){
       if(chessboard[i][j]==1){
        return false;
     }
    }
   for(int i=row-1,j=col-1;j>=0,i>=0;i--,j--){
       if(chessboard[i][j]==1){
        return false;
     }
}
return true;
}
void trackback(int row){
    if(row==n){
      for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if(chessboard[i][j]==1){
                cout<<j+1<<" ";
            }
        }
      }
      cout<<endl;
      return ;
    }
    for(int i=0;i<n;i++){
        if(isvalid(row,i)){
            chessboard[row][i]=1;
            trackback(row+1);
            chessboard[row][i]=0;
        }
    }
}
int main(){
    
    cin>>n;
    
    chessboard=vector<vector<int>>(n,vector<int>(n,0));
    
    trackback(0);
   return 0;
}

```
# 李白打酒
```cpp
#include <iostream>
using namespace std;

int t;
int ans = 0;

void track(int flower, int shop, int ac) {
    if (flower == 0 && shop == 0) {
        if (ac == 1) ans++; // 这里应该判断是否正好喝光酒
        return;
    }
    if (flower > 0 && ac >= 1) { // 喝酒前要保证酒不为负
        track(flower - 1, shop, ac - 1);
    }
    if (shop > 0) {
        track(flower, shop - 1, ac * 2);
    }
}

int main() {
    cin >> t;
    while (t--) {
        int shop, flower;
        cin >> shop >> flower;
        ans = 0;
        track(flower - 1, shop, 2); // 最后一次是花，所以先扣除1朵花
        cout << ans << endl;
    }
    return 0;
}
```
