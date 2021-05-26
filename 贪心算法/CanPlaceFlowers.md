### 605. 种花问题 https://leetcode-cn.com/problems/can-place-flowers/  
假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花不能种植在相邻的地块上，它们会争夺水源，两者都会死去。  
给你一个整数数组  flowerbed 表示花坛，由若干 0 和 1 组成，其中 0 表示没种植花，1 表示种植了花。另有一个数 n ，能否在不打破种植规则的情况下种入 n 朵花？能则返回 true ，不能则返回 false。  
示例 1：

输入：flowerbed = [1,0,0,0,1], n = 1
输出：true

示例 2：

输入：flowerbed = [1,0,0,0,1], n = 2
输出：false

提示：

    1 <= flowerbed.length <= 2 * 104
    flowerbed[i] 为 0 或 1
    flowerbed 中不存在相邻的两朵花
    0 <= n <= flowerbed.length  
 【思路】  
 不要把问题想复杂了，模拟计算机思考过程，遍历flowerbed数组过程中需要处理什么？  
 数组有哪几种情况？——1或者0  
 遇到1该怎么处理？——跳过  
 遇到0该怎么处理？——判断0下一个位置情况
 【coding】
 ```c++
 bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        for (int i = 0, len = flowerbed.size(); i < len && n > 0;) {
            if (flowerbed[i] == 1) {//当前不能种,直接往后走2格
                i += 2;
            } else if (i == flowerbed.size() - 1 || flowerbed[i + 1] == 0) {
                //此处可以种下
                n--;
                i += 2;
            } else {    //当前为空,但后面相邻已经种下,故此处不能种,直接往后走3格
                i += 3;
            }
	    }
        return n <= 0 ? true : false;
    }
 ```
