
---

layout: Leetcode 最长公共子串

title: Leetcode 最长公共子串

tags: LeetCode

categories: Web

top: 36

path: /article/1713796351

abbrlink: 1713796351



date: 2024-04-21 22:33:00


---
# Leetcode 最长公共子串



1、 最长公共子串（Longest Common Substring）要求连续。这里提供的是最长公共子串（连续的子串）的Java解法，使用动态规划的方法

~~~java
public class Solution {
    public String longestCommonSubstring(String A, String B) {
        if (A == null || B == null) return "";
        int m = A.length();
        int n = B.length();
        int maxLen = 0;
        int endIndex = 0; // 用于记录最长公共子串结束的位置
        
        // 使用一个二维数组dp来保存当前位置结尾的最长公共子串的长度
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                    if (dp[i][j] > maxLen) {
                        maxLen = dp[i][j];
                        endIndex = i; // 更新最长子串的结束位置
                    }
                }
            }
        }
        
        // 返回最长子串
        return A.substring(endIndex - maxLen, endIndex);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        // 测试示例
        String A = "abcde";
        String B = "abfce";
        System.out.println(solution.longestCommonSubstring(A, B)); // 应该输出"abc"
    }
}
~~~



这个解法中，我们使用一个二维数组`dp`来记录字符串`A`和字符串`B`的每个位置结尾的最长公共子串的长度。如果`A[i-1]`和`B[j-1]`两个字符相同，那么`dp[i][j]`就是`dp[i-1][j-1]`的基础上加1。我们同时记录下当前找到的最长子串的长度和结束位置，最后通过这两个值来截取并返回最长公共子串。



2、最长公共子序列（Longest Common Subsequence, LCS）不要求连续，

~~~java 
public class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        if (text1 == null || text2 == null) return 0;
        int m = text1.length();
        int n = text2.length();
        
        // dp[i][j]表示text1的前i个字符与text2的前j个字符的最长公共子序列长度
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    // 如果当前字符相等，则该位置的LCS长度为左上角的LCS长度加1
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    // 如果当前字符不相等，则该位置的LCS长度为左边和上边的LCS长度的最大值
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        
        // 返回整个序列的LCS长度
        return dp[m][n];
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        // 测试示例
        String text1 = "abcde";
        String text2 = "ace";
        System.out.println(solution.longestCommonSubsequence(text1, text2)); // 应该输出3
    }
}
~~~

这段代码中，我们创建了一个二维数组`dp`来记录`text1`和`text2`的每个子序列的最长公共子序列的长度。`dp[i][j]`代表`text1`的前`i`个字符和`text2`的前`j`个字符的最长公共子序列的长度。通过两层循环，我们比较每一对字符，如果字符相等，则当前位置的LCS长度为左上角的LCS长度加1；如果字符不相等，则当前位置的LCS长度为左边和上边的LCS长度的最大值。最终，`dp[m][n]`中存储的就是整个序列的最长公共子序列的长度，其中`m`和`n`分别是`text1`和`text2`的长度。