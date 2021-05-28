### 665. 非递减数列  https://leetcode-cn.com/problems/non-decreasing-array/

给你一个长度为 n 的整数数组，请你判断在 最多 改变 1 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中任意的 i (0 <= i <= n-2)，总满足 nums[i] <= nums[i + 1]。

【贪心算法】作者：Terry2020  
本题是要维持一个非递减的数列，所以遇到递减的情况时（nums[i] > nums[i + 1]），要么将前面的元素缩小，要么将后面的元素放大。  
但是本题唯一的易错点就在这，

    如果将nums[i]缩小，可能会导致其无法融入前面已经遍历过的非递减子数列；
    如果将nums[i + 1]放大，可能会导致其后续的继续出现递减；

所以要采取贪心的策略，在遍历时，每次需要看连续的三个元素，也就是瞻前顾后，遵循以下两个原则：

    需要尽可能不放大nums[i + 1]，这样会让后续非递减更困难；
    如果缩小nums[i]，但不破坏前面的子序列的非递减性；

算法步骤：

    遍历数组，如果遇到递减：
        还能修改：
            修改方案1：将nums[i]缩小至nums[i + 1]；
            修改方案2：将nums[i + 1]放大至nums[i]；
        不能修改了：直接返回false；  

【coding】
```c++
bool checkPossibility(vector<int>& nums) {
        if(nums.size() <= 2)return true;
            int count = 0;
            for(int i = 0; i < nums.size()-1; i++){
                if(nums[i] > nums[i+1]){
                    if(i == 0 || nums[i-1] < nums[i+1])  nums[i] = nums[i+1];//前面数字放大
                    else if(nums[i-1] > nums[i+1])    nums[i+1] = nums[i];   //后面数字缩小    
                    count++;         
                }  
            }
            return count < 2;
    }
```
