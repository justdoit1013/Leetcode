### 763. 划分字母区间  https://leetcode-cn.com/problems/partition-labels/

字符串 S 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一字母最多出现在一个片段中。返回一个表示每个字符串片段的长度的列表。  
示例：

输入：S = "ababcbacadefegdehijhklij"
输出：[9,7,8]
解释：
划分结果为 "ababcbaca", "defegde", "hijhklij"。
每个字母最多出现在一个片段中。
像 "ababcbacadefegde", "hijhklij" 的划分是错误的，因为划分的片段数较少。  
提示：

    S的长度在[1, 500]之间
    S只包含小写字母 'a' 到 'z' 

【思路】
乍一看想不到贪心，我只想到了区间，即应该和每个字母的[开始,结束]区间有关。之后思路就断了。  
查看官方解析后：从结果出发，如果一串字母属于同一区间，会有什么特点？  
同一区间内的字母存在区间交集，而字母的最左端和最右端确定了这个区间范围。  
所以只要知道最左端和最右端的索引，即可得到区间的长度。  
1.遍历一遍数组,统计每个字母最后出现的索引end，存入数组last  
2.依次遍历字母,让其与同区间的最右端比较{这里最右端使用max更新},直到遍历至end位置,记录此时的区间长度
【coding】
```c++
vector<int> partitionLabels(string S) {
        int last[26];
        //记录每个字符最后出现的索引
        for(int i = 0; i < S.size(); i++){
            last[S[i] - 'a'] = i;
        }
        vector<int> res; //长度统计列表
        int start = 0, end = 0;
        for(int i = 0; i < S.size(); i++){
            end = max(end, last[S[i] - 'a']);//同一个区间的最后位置
            if(i == end){   //达到结束位置,添加至返回列表
                res.push_back(end - start + 1);
                start = end + 1;
            }
        }
        return res;
    }
```
【总结】  
在处理数组前统计一遍信息（如频率，个数，第一次出现的位置，最后一次出现的位置）可以将问题转换。
