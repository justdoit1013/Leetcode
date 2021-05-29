### 1046. 最后一块石头的重量  https://leetcode-cn.com/problems/last-stone-weight/

有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块 最重的 石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x <= y。那么粉碎的可能结果如下：

    如果 x == y，那么两块石头都会被完全粉碎；
    如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。

最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。  
【coding】
```c++
方法1：多次sort排序,需要nlogn的时间复杂度，O(n)空间复杂度
int lastStoneWeight(vector<int>& stones) {
        if(stones.size() == 1)  return stones.back();
        sort(stones.begin(), stones.end());
        while(stones.size() > 1){
            int r = stones.back();
            stones.pop_back();
            int l = stones.back();
            stones.pop_back();
            if(r-l != 0)    stones.push_back(r-l);
            sort(stones.begin(), stones.end());
        }
        if(stones.size() != 0)  return stones.back();
        return 0;
 }
 
 方法2：最大最小应该优先想到堆，需要nlogn的时间复杂度，O(n)空间复杂度
 int lastStoneWeight(vector<int>& stones) {
    priority_queue<int> q;
        for (int s: stones) {
            q.push(s);
        }
        while (q.size() > 1) {
            int a = q.top();
            q.pop();
            int b = q.top();
            q.pop();
            if (a > b) {
                q.push(a - b);
            }
        }
        return q.empty() ? 0 : q.top();
 }
```
