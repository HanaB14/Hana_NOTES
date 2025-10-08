# Merge

[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)  

Remarks:
1. Comparator (Use Lambda):（`Arrays.sort(intervals, (a,b)->a[0]-b[0])`）  

2. Arrays.sort() directly modifies the order on the original array.

3. Return (List->)2D Array: toArray()
`merged.toArray(new int[merged.size()][])`
e.g. new int[3][] //建一个有3行但内容为null的二维数组
e.g. new int[3][2] //建一个“3行2列”的矩形二维数组
---

💡 Handle edge case -> Sort the intervals based on their starting points -> Iterate through the sorted intervals and check for an overlap, starting from the second one -> Return the resulting 2D array.

---
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) return intervals;

        Arrays.sort(intervals, (a,b)->Integer.compare(a[0],b[0]));
        List<int[]> merged = new ArrayList<>();
        int[] current = intervals[0];

        for(int i = 1; i < intervals.length; i++){
            if(current[1] >= intervals[i][0]){
                current[1] = Math.max(current[1],intervals[i][1]);
            }else{
                merged.add(current);
                current = intervals[i];
            }
        }
        merged.add(current);
        return merged.toArray(new int[merged.size()][]);//return 2D Array
    }
}