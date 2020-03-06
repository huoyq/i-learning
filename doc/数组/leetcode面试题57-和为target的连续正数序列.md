```java
public static int[][] findContinuousSequence(int target) {

    //枚举起始元素，因为结果中至少包含两个元素，所以枚举的最大边界为：(target - 1) / 2
    int limit = (target - 1) / 2;
    int sum = 0;
    // res用于保存最终的结果
    List<int[]> res = new ArrayList<>();
    // list用于保存一次遍历的结果集
    List<Integer> list = new ArrayList<>();

    for (int i = 1; i <= limit; i++) {
        for (int j = i;;j++ ) {
            sum += j;
            if (sum >= target) {
                if (sum == target) {
                    list.add(j);
                    Integer[] arr = new Integer[list.size()];
                    int[] arr2 = new int[list.size()];
                    list.toArray(arr);
                    // toArray方法返回的数组类型为arr的数组类型，且数组类型不能为基本类型，这里为Integer
                    // 因为最终要返回int数组类型，所以需要遍历转化为int数组。如果返回类型是list就容易多了。。。
                    for (int k = 0; k < list.size(); k++) {
                        arr2[k] = arr[k];
                    }
                    res.add(arr2);
                }
                list.clear();
                sum = 0;
                break;
            } else {
                list.add(j);
            }
        }
    }
    return res.toArray(new int[res.size()][]);
}

// 双指针+滑动窗口
public static int[][] findContinuousSequence2(int target) {
    // 窗口左边界
    int i = 1;
    // 窗口右边界
    int j = 1;
    int sum = 0;
    List<int[]> res = new ArrayList<>();
    while (i <= target / 2) {
        if (sum < target) {
            // 小于target移动右边界，并计算当前总和
            sum += j;
            j++;
        } else if (sum > target) {
            // 大于target说明当前通过左边界的值无法找到和为target的序列，移动左边界，sum剪掉之前的边界值i
            sum -= i;
            i++;
        } else {
            // 找到了，计算数组长度为j-i，循环给数组赋值
            int[] arr = new int[j-i];
            for (int k = i; k < j; k++) {
                arr[k-i] = k;
            }
            // 添加到结果集
            res.add(arr);
            // 减去之前的左边界，并使用新的边界i+1
            sum -= i;
            i++;
        }
    }
    return res.toArray(new int[res.size()][]);
}
```
