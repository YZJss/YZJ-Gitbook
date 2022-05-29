# C++ STL

### String

**str 转 int stoi(str)**

**str 转 long stol(str)**

**str 转 float stof(str)**

**char -'0' 转 int int +'0' 转char**

**to\_string(type) (任意类型转换为字符串类型)**

**str.substr(int pos = 0,int n = npos)**

**str1.insert(int pos, char\* s)**

**str+='abc' (str拼接) .append()**

**str1.find(string str2,int pos = 0)**

```
int main() {
    string s1 = "aeiouAEIOU";
    string s2 = "apple";
    int a = s1.find(s2[2]);     //从s1字符串内查找s2字符，返回查到的位置索引，反之返回-1。
    printf("a: %d", a);
    return 0;
}
```

### Vector

vector\<vector> dp(n,vector(m,0)) (n行m列 0)

**v1.push\_back() (尾插)**

**v1.pop\_back() （尾删）**

**v1.insert(const\_iterator pos, ele) (位置迭代器)**

**v1.erase(const\_iterator pos)(位置迭代器)**

**v1.assign(v.begin(),v.end()) (赋值)**

**v1.back() (最后一个元素地址)**

二维数组push\_back(一维数组)

### stack

**栈 先进后出**

**stk.push() (栈顶添加元素)**

**stk.pop() (栈顶删除元素)**

**stk.top() (返回栈顶元素)**

**stk.empty() (判断是否为空)**

**stk.size() (返回栈的大小)**

### queue

**队列 先进先出**

**que.push() (队尾添加元素)**

**que.pop() (队头移除一个元素)**

**que.back() (返回最后一个元素)**

**que.front() (返回第一个元素)**

**que.size()**

**que.empty()**

priority\_queue\<Type, Container, Functional> 优先队列 priority\_queue \<int,vector,greater > q //升序队列 priority\_queue \<int,vector,less > q //降序队列

### set

set 不允许出现重复 所有的元素都会被自动排序（默认从小到大） 不能直接修改它的元素值

multiset 允许出现键值重复

unordered\_set unordered\_multiset元素不会自动排序

**s.insert(elem)**

**s.size()**

**s.empty()**

**s.erase(pos) (迭代器) （begin,end）(区间) (elem) （值）**

**s.clear()**

**s.find(key) （查找key是否存在，存在返回迭代器，反之返回s.end()）**

**s.count(key) （统计key的个数）**

### map

**pair \<key,value> p(value1,value2)**

#### unordered\_map 无序

**迭代器 .first key .second value**

**mp.insert(pair\<int,int>(1,2))**

**mp.erase() (可以是迭代器、key)**

**mp.count(key) (0,!=0)**

**mp.find(key) (mp.end())**

ma\[x]++ count

auto 迭代器

reverse(begin(),end())

swap(a,b)

**sort(begin(),end())**

sort函数根据comp函数的返回值，对comp函数的两个参数排序。如果comp返回true，排序为“参数1”“参数2”，否则排序为“参数2”“参数1”。 想要升序排列，则return parameter1\<parameter2，想要降序排列，则return parameter1>parameter2

```
//c++内置比较函数
less<type>() 		// <
greater<type>() 	// >
less_equal<type>()	// <=
gtater_equal<type>()// >=
```

**\*max\_element(begin(),end())**

**\*min\_element(begin(),end())**

**accumulate(begin(),end(),0) (求和)**

INT\_MAX INT\_MIN

LLONG\_MAX LLONG\_MIN
