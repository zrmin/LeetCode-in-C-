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

   ```c++
   ```

   

7. 整数反转

   ```C++
   ```

   

8. 字符串转换整数（atoi）

   ```C++
   ```

   

9. 回文数

   ```C++
   ```

   

10. 正则表达式匹配

    ```c++
    ```

    