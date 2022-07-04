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
    ```

    

14. 最长公共前缀

    ```C++
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

    