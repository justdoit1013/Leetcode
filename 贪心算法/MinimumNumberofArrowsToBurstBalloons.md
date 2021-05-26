### 452. 用最少数量的箭引爆气球 https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/

在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以纵坐标并不重要，因此只要知道开始和结束的横坐标就足够了。开始坐标总是小于结束坐标。

一支弓箭可以沿着 x 轴从不同点完全垂直地射出。在坐标 x 处射出一支箭，若有一个气球的直径的开始和结束坐标为 xstart，xend， 且满足  xstart ≤ x ≤ xend，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。

给你一个数组 points ，其中 points [i] = [xstart,xend] ，返回引爆所有气球所必须射出的最小弓箭数。  

【思路】  
找重复区间，重复区间内的可以用一支箭引爆  
为此每次遍历到新区间时，需要判断此时是否与原来的重叠区间有交集，有则一波带走，没有则重新确定重叠区间
【coding】
```c++
int findMinArrowShots(vector<vector<int>>& points) {
        if(points.size() <= 1)  return points.size();
        int count = 1;
        sort(points.begin(), points.end(), [](vector<int> a, vector<int> b){
            return a[1] < b[1];//按末尾升序
        });
        //优化：记录两个重叠区间左右端点,后面依次判断即可,不在区间内则重新确定区间
        //O(n)
        int len = points.size();
        int left = points[0][0], right = points[0][1];//可以一波带走的重叠区间
        for(int i = 1; i < len; i++){
            if(points[i][0] <= right && points[i][0] >= left){
                left = points[i][0];//更新左区间
            } 
            else if(points[i][0] > right){//重新记录可一波带走的区间
                count++;
                left = points[i][0];
                right = points[i][1];
            }
        }
        return count;
    }
```
