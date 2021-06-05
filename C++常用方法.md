### 范围
```c++
unsigned int       0～4294967295   
int                 -2147483648～2147483647 
unsigned long       0～4294967295
long                -2147483648～2147483647
long long的最大值：  9223372036854775807
long long的最小值：  -9223372036854775808
unsigned long long的最大值：1844674407370955161
1ull ——> unsigned long long
```

### 宏定义
```c++
#define INT_MAX 2147483647
#define INT_MIN (-INT_MAX - 1)
const M = 1e9+7  %大数用于取余防止溢出
1e9   ---10^9
1e6+7 ---10^6+7
```

### 常用函数
```c++
//元素比较大小
max(a,b);
min(a,b);
//数组最值
*max_element(iterator first, iterator last);
*min_element(iterator first, iterator last);
//数组合并,result为新数组
merge (InputIterator1 first1, InputIterator1 last1,
       InputIterator2 first2, InputIterator2 last2,
       OutputIterator result);
//逆序
void reverse(vector<int>& nums, int left, int right);  //首尾交换实现的
//数组旋转
rotate(vec.begin(), vec.begin()+k, vec.end());
例如k = 3
1 2 3 4 5 6 7 8 9
4 5 6 7 8 9 1 2 3
//vector初始化
void fill (ForwardIterator first, ForwardIterator last, const T& val);
//交换数组，这里的arr可以是普通数组也可以是vector
swap(arr,arr1)//常量时间复杂度,这里的arr可以int arr[]定义的,也可以是vector定义的
//二分查找
  //int a[];
  upper_bound(a+i,a+j,x)-a;    //返回第一个大于x的数的位置
  lower_bound(a+i,a+j,x)-a;    //返回第一个大于等于x的数的位置
  //vector<int> a;
  lower_bound(a.begin(), a.end(), x)-a.begin();
  upper_bound(a.begin(), a.end(), x)-a.begin();
  
  binary_search(a.begin(), a.end(), x);//返回值为bool类型,注意数组的前提是有序
 
//一维排序
sort(a,a+n);                 //int a[]
sort(num.begin(), num.end());//vector<int> num 

//二维排序
按照第二个字段排序
sort(num.begin(), num.end(), [](vector<int> a,vector<int> b){return a[1]<b[1];});
按照第一个字段排序
sort(num.begin(), num.end(), [](vector<int> a,vector<int> b){return a[0]<b[0];});
联合排序
sort(logs.begin(), logs.end(), [](vector<int> a,vector<int> b){
     if(a[0] != b[0])    
         return a[0]<b[0];
     else return a[1] < b[1];
}); 
默认升序
sort(num.begin(),num.end(),greater<int>());   //less<int>()：升序,greater<int>():降序
//复制
copy(a.begin(),a.end(),b.begin())
```

### vector
```c++
insert(iterator positionn,value)     //arr.position或者是iterator position
insert(iterator position,size,value) //size是插入几个该数
push_back(elem)//插入
pop_back()     //弹出
size()
front()        //获取首元素，不弹出
back()         //获取最后元素，不弹出
empty()
erase(iterator it);
at(int index)  //索引访问
//遍历
begin(),end()  //从前往后遍历--从小到大
rbegin(),rend()//从后往前遍历--从大到小

//1.C++迭代器遍历 
for(vector<int>::iterator it = nums.begin(); it < nums.end(); it++){
  cout<<*it<<" "; //迭代器是指向堆中的地址【类似java实现】
}
//2.C++迭代器遍历 
vector<int>::iterator v = res.begin();
while(v!=res.end()){
  cout<<*v<<endl;
  v++;}
```

### set  
```c++
元素唯--一去重,有序--红黑树
定义集合set:
1.set<int> s;
2.还可以把一个数组放进去：set<int> s(arr.begin(),arr.end());
set方法：
1.insert(elem)  向set容器中插入元素，无返回值
  insert(pos,elem) 指定pos插入elem
2.erase(elem)   按元素值删除元素，无返回值
  erase(iterator pos)    移除pos所指元素位置，无返回值,这里的pos是迭代器指针
  erase(iterator begin, iterator end)移除begin,end区间内所有元素，无返回值

3.begin()   容器中第一个元素的索引，*(s.begin())为该元素的值
4.end()     指向容器中最后一个元素的下一位
5.rbegin()  容器中最后一个元素的索引
6.rend()    容器中第一个元素的索引

7.size()    set容器的大小
10.empty()  容器是否为空，空为true
11.clear()  清空容器

8.find(elem)   返回被查找到元素在原数组中是第一个被插入的,返回索引
9.count(elem)  返回某个元素出现的个数

12.upper_bound(elem)  返回元素值>elem的第一个元素位置
13.lower_bound(elem)  返回元素值>=elem的第一个元素位置
14.equal_range(elem)  返回元素值==elem的区间
```

### multiset同set方法，有序且允许重复。  
```c++
int main() {
    multiset<int> st;
    vector<int> nums = {1,4,5,7,2,5};
    //插入元素
    for(int i = 0; i < nums.size(); i++){
        st.insert(nums[i]);
    }
    //遍历迭代器
    multiset<int>::iterator it;
    for(it = st.begin(); it != st.end(); it++){
		printf("%d ",*it); //会将存放的元素全部输出
	  }
    st.erase(st.find(2));//find-找到元素为2的索引,erase-删除
    cout<<endl;
    for(it = st.begin(); it != st.end(); it++){
		printf("%d ",*it); //会将存放的元素全部输出
	 } 
    cout<<endl;
    //元素最大最小值
    cout<<*st.begin()<<" "<<*st.rbegin();
    return 0;
}

```
### unordered_map  
```c++
http://www.cplusplus.com/reference/unordered_map/unordered_map/at/
内部实现哈希表，查询快速，与map用法相同
插入
insert(pair<,>());
map[index]=?;
map.insert(m.begin(),m.end());
查找
find()//返回迭代器值
count()//记数,也可以用于判断是否已经存在
修改
map.at("shioas") = 312;

遍历
begin()
end()
iter->first
iter->second

int main() {
    //初始化与插入
    unordered_map<int,string> myMap = {{ 0, "张大" },{ 1, "李五" }};
    myMap[2] = "xixi";
    //①
    myMap.insert(pair<int, string>(3, "陈二"));
    //②
    // pair<int, string> myshopping (5,"baking powder");
    // unordered_map<int,string> myMap1;
    // myMap1.insert(myshopping);
    
    // myMap1.insert(myMap.begin(),myMap.end());//插入至新map
    //遍历
    for(auto iter = myMap.begin(); iter != myMap.end(); iter++){
        cout << iter->first << "," << iter->second << endl;  
    }
    //查找find，返回迭代器
    auto iterator = myMap.find(2);//find()返回一个指向2的迭代器
    if (iterator != myMap.end())
	    cout << endl<< iterator->first << "," << iterator->second << endl;  
    return 0;
}
```
### 字符串
```c++
字符串长度
string s;
int len = s.length();
普通数组长度
int len = sizeof(arr)/sizeof(arr[0]);
vector长度
int len = arr.size();
```

### 栈、队列
```c++

```


