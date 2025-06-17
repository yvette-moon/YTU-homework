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
