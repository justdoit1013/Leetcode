### 860. 柠檬水找零  https://leetcode-cn.com/problems/lemonade-change/

在柠檬水摊上，每一杯柠檬水的售价为 5 美元。

顾客排队购买你的产品，（按账单 bills 支付的顺序）一次购买一杯。

每位顾客只买一杯柠檬水，然后向你付 5 美元、10 美元或 20 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 5 美元。

注意，一开始你手头没有任何零钱。

如果你能给每位顾客正确找零，返回 true ，否则返回 false   
【思路】  
优先选择面值高的找出零钱  
关键是如何实现，我思路比较堵塞，开始只想到用multiset有序存储币值,借助multiset的有序和find查找功能，但是实现起来反而更复杂，也走了很多弯路。  
其实只需要看目前有没有可以兑换的币种就可以了，这样只需要记录一下币种的数量即可。  
【coding】  
```c++
bool lemonadeChange(vector<int>& bills) {
        //优先把大币值兑出去,能兑换的只有5元和10元
        int five = 0, ten = 0;
        for(int i = 0; i < bills.size(); i++){
            if(bills[i] == 5)  five++;
            else if(bills[i] == 10){//找钱5元
                ten++;
                if(five-1 < 0)  return false;//找5元
                else five--;
            } 
            else{//找钱15元
                if(ten-1 >= 0 && five-1 >= 0){//先10后5
                    ten--;
                    five--;
                }
                else if(five-3 >= 0){//3个5
                    five -= 3;
                }   
                else return false;
            } 
        }
        return true;
    }
```
