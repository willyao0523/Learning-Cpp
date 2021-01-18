## Leetcode 89 - 格雷码

格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个位数的差异。

给定一个代表编码总位数的非负整数 n，打印其格雷编码序列。即使有多个不同答案，你也只需要返回其中一种。

格雷编码序列必须以 0 开头。

示例 1:
```
输入: 2
输出: [0,1,3,2]
解释:
00 - 0
01 - 1
11 - 3
10 - 2

对于给定的 n，其格雷编码序列并不唯一。
例如，[0,2,3,1] 也是一个有效的格雷编码序列。

00 - 0
10 - 2
11 - 3
01 - 1
```

示例 2:
```
输入: 0
输出: [0]
解释: 我们定义格雷编码序列必须以 0 开头。
     给定编码总位数为 n 的格雷编码序列，其长度为 2n。当 n = 0 时，长度为 20 = 1。
     因此，当 n = 0 时，其格雷编码序列为 [0]。
```

### C++
- 1
```c++
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> ans;
        for(int i = 0; i < (1 << n); i++) {
            // 格雷码公式: i ^ (i >> 1)
            ans.push_back(i ^ (i >> 1));
        }
        return ans;
    }
};
```

- 2
```c++
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<vector<int>> dp(n + 1);
        dp[0] = {0};    
        for (int i = 1; i <= n; ++i) {
            dp[i] = dp[i - 1];
            for (int j = dp[i - 1].size() - 1; j >= 0; --j)
                dp[i].push_back(dp[i - 1][j] | (1 << (i - 1)));
            }
        return dp[n];
    }
};
```