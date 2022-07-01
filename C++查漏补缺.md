<h1><center>LeetCode C++查漏</center></h1>

## 一、unordered_map

unordered_map是C++中的方法。

用于通过指定key对unordered_map中存在的元素数量进行计数。但是由于unordered_map中不允许存储具有相同键的元素，因此count()函数本质上检查unordered_map中是否存在具有给定键的元素。

```c++
unordered_map<int, int> hash;
hash.count(key); // 如果hash中存在具有给定键的值，则返回1，否则返回0
```

题目：<a href = "https://leetcode-cn.com/problems/two-sum/">LeetCode第一题</a>



## 二、substr

substr()是C++字符串函数，主要用于复制子字符串，要求从指定位置开始，并具有指定长度。

如果没有指定长度，或者长度超过了原串末尾，则子字符串将延续到字符串末尾。

```c++
string res;
if(res.size() < (r -1) - (l + 1) - 1) res = s.substr(l + 1, (r - 1) - (l + 1) + 1);
```

题目：<a href = "https://leetcode-cn.com/problems/longest-palindromic-substring/">LeetCode第五题</a>



### 三、INT_MAX、INT_MIN、

在头文件limits.h中

题目：<a href="https://leetcode-cn.com/problems/reverse-integer/">LeetCode第七题</a>

```c++
if(x > 0 && res > (INT_MAX - x%10)/10) return 0;
if(x < 0 && res < (INT_MIN - x%10)/10) return 0;
```

负数比正数的绝对值大一，所以，res存不下负数的INT_MIN。所以如果用res存储正负数的绝对值的话，需要特判一下负无穷INT_MIN这种情况。

```c++
if (-res * 10 - (s[k] - '0') == INT_MIN) return INT_MIN;
```

题目：<a href="https://leetcode-cn.com/problems/string-to-integer-atoi/">LeetCode第八题</a>



## 四、to_string

to_string是C++11新增的，用于将int转换成string。

```c++
int x;
string s = to_string(x);
```

题目：<a href="https://leetcode-cn.com/problems/palindrome-number/">LeetCode第九题</a>



## 五、C++删除string最后一个字符的几种办法

1. ```c++
   // 使用substr
   string str;
   str = str.substr(0, str.length() - 1);
   ```

2. ```c++
   // 使用erase
   string str;
   str.erase(str.end() - 1);
   ```

3. ```c++
   // 使用pop_back()
   string str;
   str.pop_back();
   ```

   题目：<a href="https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/">LeetCode第十七题</a>



## 六、倒数第N+1个点

倒数第$n+1$个点，是正数的第$n-k$个点。

因为：下标从0开始，总共有cnt个点，下标从0 ~ cnt-1，倒数第$n+1$个点，则该点前面还有$cnt - (k+1)$个点，下标从$0$~$cnt-(k+1) - 1$，即倒数第$n+1$个点的前一个点的下标为$cnt-k-2$，则倒数第$n+1$个点的下标为$cnt-k-1$，由于小标是从0开始的，所以它是正数的第$cnt-k$个点。

题目：<a href="https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/">LeetCode第十九题</a>



## 七、有效括号序列的性质

1. '('的数量一定>=')'的数量

2. '('的数量==')'的数量

   题目：<a href="https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/">LeetCode第题</a>



## 八、旋转图像的转换

1. 顺时针90：
   * 主对角线（从左上到右下）翻转
   * 从中间竖直左右翻转
2. 逆时针90：
   * 主对角线翻转
   * 从中间上下翻转
3. 顺时针180或逆时针180：
   * 主对角线翻转
   * 副对角线翻转

题目：<a href="https://leetcode-cn.com/problems/rotate-image/">LeetCode第48题</a>



## 九、stringstream

库名：<sstream>

stringstream用来进行流的输入输出操作。

```c++
stringstream ssin(s);
int res = 0;
string word;
while(ssin >> word) res = word.size(); // 获取字符串s中的最后一个单词的长度
```

题目：<a href="https://leetcode-cn.com/problems/length-of-last-word/">LeetCode第58题</a>



## 十、next_permutation

获取下一个全排列。

next_permutaion有两种原型：

```c++
template<class Iterator>
  bool next_permutation (Iterator first, Iterator last);

template<class Iterator, class Compare>
  bool next_permutation (Iterator first, Iterator last, Compare comp);
```

next_permutation是一个原地算法（会直接改变这个集合，而不是返回一个集合），它对一个可以遍历的集合（如string，如vector），将**迭代器范围** [first, last] 的排列 排列到下一个排列（第一个是名词，第二个是动词，第三个是名词），其中所有排列的集合默认按照operator < 或者 字典序 或者 按照输入到第三个参数 comp 的排列方法排列。如果存在这样的“下一个排列”，返回true并执行排列，否则返回false。

题目：<a href="https://leetcode-cn.com/problems/permutation-sequence/">LeetCode第60题</a>
