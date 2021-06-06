### 435. 无重叠区间medium https://leetcode-cn.com/problems/non-overlapping-intervals/

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

注意:

    可以认为区间的终点总是大于它的起点。
    区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

【思路】
在选择要保留区间时，区间的结尾十分重要：选择的区间结尾越小，余留给其它区间的空间
就越大，就越能保留更多的区间。因此，我们采取的贪心策略为，优先保留结尾小且不相交的区
间。  
【coding】  
```c++
int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        //特殊情况
        if(intervals.empty() || intervals.size() == 1)   return 0;
        //按末尾升序
        sort(intervals.begin(), intervals.end(),[](vector<int> a,vector<int> b){
            return a[1] < b[1];//升序
        });
        //边界
        int count = 0;//需移除的区间个数
        int index = 0;//前面确定区间的索引
        for(int i = 1; i < intervals.size(); i++){
            if(intervals[i][0] < intervals[index][1]) count++;//移除当前区间
            //标记索引
            else index = i;
        }
        return count;
    }
```  

类题  
### HDU:http://acm.hdu.edu.cn/showproblem.php?pid=2037  
目标是能看尽量多的完整节目
Input
输入数据包含多个测试实例，每个测试实例的第一行只有一个整数n(n<=100)，表示你喜欢看的节目的总数，然后是n行数据，每行包括两个数据Ti_s,Ti_e (1<=i<=n)，分别表示第i个节目的开始和结束时间，为了简化问题，每个时间都用一个正整数表示。n=0表示输入结束，不做处理。  
Output  
对于每个测试实例，输出能完整看到的电视节目的个数，每个测试实例的输出占一行。  
Sample Input  
12  
1 3  
3 4  
0 7  
3 8  
15 19  
15 20  
10 15  
8 18  
6 12  
5 10  
4 14  
2 9  
0  
Sample Output  
5  
```c++
#include<iostream>
#include <algorithm>
#include<cstdlib>
#include<cstdio>
using namespace std;
typedef struct time
{
    int a;
    int b;
}t;
//二维排序
int cmp(const void* a,const void* b)
{
   struct time *c = (time *)a;
   struct time *d = (time *)b;
   return c->b-d->b;//不相等，按结束时间升序 
}
t time[101];
int main()
{
    int n,i;
    while(scanf("%d",&n)!=EOF && n)
    {
     int sum=0,nowtime=0;
     for(i=0;i<n;i++)
      cin>>time[i].a>>time[i].b;   
      // 排序
     qsort(time, n, sizeof( time[0]), cmp);
     // 选择区间
    for(i=0; i<n; i++)
    {
        if(time[i].a >= nowtime)
        {
            nowtime = time[i].b;
            sum++;
        }
    }
    cout<<sum<<endl;    
    }
        return 0;
 } 
```  




