```java
// 递归 会超时，因为递归过程中有大量的重复计算
// 例如计算f(n)=f(n-1)+f(n-2)时，f(n-1)=f(n-2)+f(n-3)，f(n-2)=f(n-3)+f(n-4)
// f(n-3)被重复计算了两次
public static int numWays(int n) {
    if (n == 0) {
        return 1;
    } else if (n == 1) {
        return 1;
    } else {
        return (numWays(n-1) + numWays(n-2)) % 1000000007;
    }
}

// 动态规划空间复杂度O(n)
public int numWays2(int n) {
    if (n == 0) {
        return 1;
    }
    int[] dp = new int[n+1];
    dp[0] = 1;
    dp[1] = 1;
    // 计算数组每个下标位置的值，等于前两个元素之和
    for (int i = 2;i <= n;i++) {
        dp[i] = (dp[i-1] + dp[i-2]) % 1000000007;
    }
    // 数组中最后元素为最终结果
    return dp[n];
}

// 动态规划空间复杂度O(1)
public static int numWays3(int n) {
    int a = 1; // 相当于f(0) = 1;
    int b = 1; // 相当于f(1) = 1;
    int sum;
    for (int i = 1; i <= n; i++) {
        sum = (a + b) % 1000000007;
        a = b;
        b = sum;
    }
    return a;
}

```
