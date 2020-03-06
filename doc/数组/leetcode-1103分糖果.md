```java
public static int[] distributeCandies(int candies, int num_people) {
    int[] arr = new int[num_people];
    // count表示第几轮分配
    int count = 0;
    while (candies > 0) {
        count++;
        for (int i = 0; i < num_people; i++) {
            // 计算当前位置应该分配多少糖果
            int value = (count-1) * num_people + i + 1;
            // 若糖果不足，将剩余糖果分配给当前位置并返回
            if (candies <= value) {
                arr[i] = arr[i] + candies;
                return arr;
            }
            arr[i] = arr[i] + value;
            // 计算剩余糖果数
            candies -= value;
        }
    }
    return arr;
}

public static int[] distributeCandies2(int candies, int num_people) {
    int[] ans = new int[num_people];
    int i = 0;
    while (candies != 0) {
        // 本次应该分配的糖果数，正常情况下应该是i+1，如果糖果不足，则将剩余糖果全部分配给当前位置
        int min = Math.min(candies,i + 1);
        // 这里用了取模运算，计算位置
        ans[i % num_people] += min;
        // 剩余糖果数
        candies -= min;
        // 将i+1然后进行下一次分配
        i++;
    }
    return ans;
}
```
