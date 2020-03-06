```java
public int compareVersion(String version1, String version2) {

    // 将字符串按点好分割，生成数组和每位进行比较
    // 因为点号在正则中有特殊含义，所以需要进行转义
    String[] arr1 = version1.split("\\.");
    String[] arr2 = version2.split("\\.");
    int len1 = arr1.length;
    int len2 = arr2.length;

    // 按最长的数组进行遍历，另外一个数组长度不够用0补上
    for (int i = 0;i < (Math.max(len1, len2));i++) {
        int x = (i < len1 ? Integer.valueOf(arr1[i]) : 0);
        int y = (i < len2 ? Integer.valueOf(arr2[i]) : 0);
        if (x > y) {
            return 1;
        }
        if (x < y) {
            return -1;
        }
    }
    return 0;
}
```
