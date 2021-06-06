### 135. 分发糖果(hard) https://leetcode-cn.com/problems/candy/
老师想给孩子们分发糖果，有 N 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。

你需要按照以下要求，帮助老师给这些孩子分发糖果：

每个孩子至少分配到 1 个糖果。
评分更高的孩子必须比他两侧的邻位孩子获得更多的糖果。
那么这样下来，老师至少需要准备多少颗糖果呢？

【coding】
```c++
class Solution {
public:
    int candy(vector<int>& ratings) {
        //至少有一个糖果,故初始化为1
        vector<int> num(ratings.size(), 1);
        //两次遍历
        //第一次:处理右边孩子比左边高的情况
        for(int i = 1 ; i < ratings.size(); i++){
            if(ratings[i] > ratings[i-1])   num[i] = num[i-1] + 1;  
        }
        for(int i = ratings.size()-2; i >= 0; i--){
            if(ratings[i] > ratings[i+1] && num[i] <= num[i+1])   num[i] = num[i+1] + 1;
        }
        //求和函数
        return accumulate(num.begin(), num.end(), 0);
    }
};
```
