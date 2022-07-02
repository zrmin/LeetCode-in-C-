<center><h1>LeetCode 1~10题</h1></center>

1. 两数之和

   当遍历到一个数时，我们在unordered_map中查找有没有target-nums[i]这个数，如果有的话，就输出答案，若没有，则把当前遍历到的数加入unordered_map中。

   ```C++
   class Solution {
   public:
       vector<int> twoSum(vector<int>& nums, int target) {
           unordered_map<int, int> map;
           for(int i = 0; i < nums.size(); ++i) {
               int a = target - nums[i];
               if(map.count(a)) return {map[a], i};
               else {
                   map[nums[i]] = i;
               }
           }
   
           return {};
       }
   };
   ```

   

2. 两数相加

   其实就是用链表来做整数的加法，每个链表的节点值代表一个数位。

   遍历两个链表，其中任一个链表没有遍历完时，那么就计算这个数位上的结果。

   创建虚拟头节点，可以不用特判插入的第一个节点。

   ```C++
   /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode() : val(0), next(nullptr) {}
    *     ListNode(int x) : val(x), next(nullptr) {}
    *     ListNode(int x, ListNode *next) : val(x), next(next) {}
    * };
    */
   class Solution {
   public:
       ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
           auto dummy = new ListNode(-1), cur = dummy;
           int c = 0;
           while(l1 || l2 || c) {
               if(l1) c += l1->val, l1 = l1->next;
               if(l2) c += l2->val, l2 = l2->next;
               cur->next = new ListNode(c%10);
               cur = cur->next;
               c /= 10;
           }
   
           return dummy->next;
       }
   };
   ```

   

3. 无重复字符的最长子串

   双指针算法：用两个指针i和j同时遍历字符串s，i在前，j在后，用哈希表维护j到i之间的每个字符出现的个数。然后看j到i之间的字符串中的每个字符的个数是否>1，若大于1，则意味着有重复字符了，而且这个重复字符就是“走”在前面的i指针指向的那个字符。然后将j往前移动，直到j到i之间的每个字符的个数都为1。此时，j到i的字符串就是无重复字符的子串。

   ```C++
   class Solution {
   public:
       int lengthOfLongestSubstring(string s) {
           unordered_map<char, int> map;
           int res = 0;
           for(int i = 0, j = 0; i < s.size(); ++i) {
               map[s[i]]++;
               while(map[s[i]] > 1) {
                   map[s[j]]--;
                   ++j;
               }
               res = max(res, i - j + 1);
           }
   
           return res;
       }
   };
   ```

   

4. 寻找两个正序数组的中位数

   ```c++
   class Solution {
   public:
       double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
           int tot = nums1.size() + nums2.size();
           if(tot % 2 == 0) {
               int left = find(nums1, 0, nums2, 0, tot/2);
               int right = find(nums1, 0, nums2, 0, tot/2 + 1);
               return (left + right) / 2.0;
           }
           else {
               return find(nums1, 0, nums2, 0, tot/2 + 1);
           }
       }
   
       int find(vector<int>& nums1, int i, vector<int>&nums2, int j, int k) {
           if(nums1.size() - i > nums2.size() - j) return find(nums2, j, nums1, i, k);
           if(k == 1) {
               if(i == nums1.size()) return nums2[j];
               else return min(nums1[i], nums2[j]);
           }
           if(i == nums1.size()) return nums2[j+k-1];
   
           int si = min(i + k/2, (int)nums1.size()), sj = j + k - k/2;
           if(nums1[si-1] > nums2[sj-1]) return find(nums1, i, nums2, sj, k - (sj - j));
           else return find(nums1, si, nums2, j, k - (si - i));
       }
   };
   ```

   

5. 最长回文子串

   ```c++
   class Solution {
   public:
       string longestPalindrome(string s) {
           string res;
           for(int i = 0; i < s.size(); ++i) {
               int l = i - 1, r = i + 1;
               while(l >= 0 && r < s.size() && s[l] == s[r]) --l, ++r;
               if(res.size() < (r-1) - (l+1) + 1) res = s.substr(l + 1, r-l-1);
   
               l = i, r = i + 1;
               while(l >= 0 && r < s.size() && s[l] == s[r]) --l, ++r;
               if(res.size() < r-l-1) res = s.substr(l + 1, r-l-1);
           }
   
           return res;
       }
   };
   ```

   

6. Z字形变换

   这是找规律的题目，从下标入手。第一行和最后一行的公差都是2*n-2，其余行是两个等差数列交错的，他们的公差都是2*n-2，交错的数列的首项是i，第二个等差数列的首项是2*n-2-i。

   ```c++
   class Solution {
   public:
       string convert(string s, int n) {
           if(n == 1) return s;
   
           string res;
           for(int i = 0; i < n; ++i) {
               if(i == 0 || i == n - 1) {
                   for(int j = i; j < s.size(); j += 2*n - 2) {
                       res += s[j];
                   }
               }
               else {
                   for(int j = i, k = 2*n-2-i; j < s.size() || k < s.size(); j += 2*n-2, k += 2*n-2) {
                       if(j < s.size()) res += s[j];
                       if(k < s.size()) res += s[k];
                   }
               }
           }
   
           return res;
       }
   };
   ```

   

7. 整数反转

   将整数中的每个数位拆分出来，并逆序组合，在组合之前，还要判断即将组合而成的数是否溢出，针对溢出，需要考虑正数和负数两种情况。

   ```C++
   class Solution {
   public:
       int reverse(int x) {
           int res = 0;
           while(x) {
               if(x > 0) if(res > (INT_MAX - x%10)/10) return 0;
               if(x < 0) if(res < (INT_MIN - x%10)/10) return 0;
               res = res*10 + x%10;
               x /= 10;
           }
   
           return res;
       }
   };
   ```

   

8. 字符串转换整数（atoi）

   首先要把字符串前面的空格除掉（有可能字符串都是空格）。然后还要判断正负。

   接着字符串分解，组合成整数，在组合成整数前，需要分，正负号判断是否越界。由于在分解字符串的过程中，res是整数，也就是说我们是按照绝对值的方式来计算整数的大小的，我们知道负数的绝对值比正数的绝对值大1，所以如果负数的res正好等于INT_MIN，那么下面的res = res * 10 + (s[k] - '0')是正数，它是会溢出的，所以需要对-res==INT_MIN进行特判。

   ```C++
   class Solution {
   public:
       int myAtoi(string s) {
           int k = 0;
           while(s[k] == ' ' && k < s.size()) k++;
           if(k == s.size()) return 0;
   
           int minus = 1;
           if(s[k] == '-') minus = -1, k++;
           else if(s[k] == '+') k++;
   
           int res = 0;
           while(k < s.size() && s[k] >= '0' && s[k] <= '9') {
               if(minus == 1) if(res > (INT_MAX - (s[k] - '0')) / 10) return INT_MAX;
               if(minus == -1) if(-res < (INT_MIN + (s[k] - '0')) / 10) return INT_MIN; 
               if(-res*10 - (s[k] - '0') == INT_MIN) return INT_MIN;
               res = res * 10 + (s[k] - '0');
               k++;
           }
   
           res = res*minus;
           if(res < INT_MIN) return INT_MIN;
           if(res > INT_MAX) return INT_MAX;
   
           return res;
       }
   };
   ```

   

9. 回文数

   这题还是可以用整数分解来做，而且没有要求int，所以可以用long long来存储翻转后的正整数，然后比较翻转后的数和原始的数是否相等。

   ```C++
   class Solution {
   public:
       bool isPalindrome(int x) {
           if(x < 0) return false;
           int y = x;
           long long res = 0;
           while(x) {
               res = res * 10 + x % 10;
               x /= 10;
           }
   
           return res == y;
       }
   };
   ```

   

10. 正则表达式匹配

    ```c++
    ```

    