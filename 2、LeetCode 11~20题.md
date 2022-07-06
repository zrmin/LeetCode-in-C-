<center><h1>LeetCode 11~20题</h1></center>

11. 盛最多水的容器

    ```C++
    class Solution {
    public:
        int maxArea(vector<int>& height) {
            int res = 0;
            for(int i = 0, j = height.size() - 1; i < j; ) {
                res = max(res, min(height[i], height[j]) * (j - i));
                if(height[i] > height[j]) --j;
                else ++i;
            }
    
            return res;
        }
    };
    ```

    

12. 整数转罗马数字

    ```c++
    class Solution {
    public:
        string intToRoman(int num) {
            string res;
    
            int number[] = {
                1000,
                900, 500, 400, 100,
                90, 50, 40, 10,
                9, 5, 4, 1
            };
    
            string roman[] = {
                "M",
                "CM", "D", "CD", "C",
                "XC", "L", "XL", "X",
                "IX", "V", "IV", "I"
            };
    
            for(int i = 0; i <= 12; ++i) {
                while(num >= number[i]) {
                    res += roman[i];
                    num -= number[i];
                } 
            }
    
            return res;
        }
    };
    ```

    

13. 罗马数字转整数

    ```C++
    class Solution {
    public:
        int romanToInt(string s) {
            unordered_map<char, int> map;
            map['I'] = 1;
            map['V'] = 5;
            map['X'] = 10;
            map['L'] = 50;
            map['C'] = 100;
            map['D'] = 500;
            map['M'] = 1000;
    
            int res = 0;
            for(int i = 0; i < s.size(); ++i) {
                if(i+1 < s.size() && map[s[i]] < map[s[i+1]]) res -= map[s[i]];
                else res += map[s[i]];
            }
    
            return res;
        }
    };
    ```

    

14. 最长公共前缀

    ```C++
    class Solution {
    public:
        string longestCommonPrefix(vector<string>& strs) {
            string res;
            if(strs.empty()) return res;
    
            for(int i = 0; ; i++) {
                if(i >= strs[0].size()) return res;
                char c = strs[0][i];
                for(string& str: strs) {
                    if(i >= str.size() || str[i] != c) return res;
                }
    
                res += c;
            }
    
            return res;
        }
    };
    ```

    

15. 三数之和

    ```C++
    ```

    

16. 最接近的三数之和

    ```C++
    ```

    

17. 电话号码的字母组合

    ```C++
    ```

    

18. 四数之和

    ```C++
    ```

    

19. 删除链表的倒数第N个结点

    ```C++
    ```

    

20. 有效的括号

    ```C++
    ```

    