贪心算法采用贪心的思想，保证每次操作都是局部最优的，从而使最后得到的结果是全局最优的。

11、盛最多水的容器(container-with-most-water)

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0;
        int right = height.size() - 1;
        int ans = 0;
        while (left < right) {
            ans = max(ans, (right - left) * min(height[left], height[right]));
            if (height[left] > height[right]) right--;
            else left++;
        }
        return ans;
    }
};
```

其中`max`和`min`函数的头文件为`<algorithm>`。

思路为首先用两个指针指向两端，再将两个指针逐步向中间移动，每次选择高度较低的一侧移动，以保证舍去的容器比保留的容器小，以此来达到局部最优，循环操作最终达到全局最优，时间复杂度为$O(n)$，如果采用暴力穷举的话时间复杂度为$O(n^2)$。

改进：快速跳过以加速：

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0;
        int right = height.size() - 1;
        int ans = 0; 
        while (left < right) {
            int minH = min(height[left], height[right]);
            ans = max(ans, (right - left) * minH);
            while (height[left] <= minH && left < right) {
                left++;
            }
            while (height[right] <= minH && left < right) {
                right--;
            }
        }
        return ans;
    }
};
```

44、通配符匹配(wildcard-matching)

回溯：

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int sn = s.length();
        int pn = p.length();
        int i = 0;
        int j = 0;
        int start = -1;
        int match = 0;
        while (i < sn) {
            if (j < pn && (s[i] == p[j] || p[j] == '?')) {
                i++;
                j++;
            }
            else if (j < pn && p[j] == '*') {
                start = j;
                match = i;
                j++;
            }
            else if (start != -1) {
                j = start + 1;
                match++;
                i = match;
            }
            else {
                return false;
            }
        }
        while (j < pn) {
            if (p[j] != '*') return false;
            j++;
        }
        return true;
    }
};
```

动态规划：

`dp[x][y]`表示对`s`和`p`各截取前`x`和前`y`个字母的匹配情况。

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.length();
        int n = p.length();
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        
        dp[0][0] = true;
        
        for (int j = 1; j <= n; j++) {
            if(p[j - 1] == '*') dp[0][j] = true;
            else break;
        }
        
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p[j - 1] == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                }
                else if (p[j - 1] == '?' || s[i-1] == p[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                else {
                    dp[i][j] = false;
                }
            }
        }
        
        return dp[m][n];
    }
};
```

