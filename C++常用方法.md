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


