# 5.28打卡
# leetcode 974
```java
/**
*思路：通过前缀和+hash表的方法来解决
* sum(i,j) = p[j] - p[i-1]，p[i]表示0到i闭区间的和
* 如果sum(i,j)%k = (p[j]-p[i-1])%m =0
* 根据同余策略，即p[j]%m==p[i-1]%m时，上式成立
* (条件：m为正整数，p[j],p[i-1]为整数，所以对于负数也成立，所以负数取余的时候要返回正数的余数)
* 注：对于负数取余，他也是有对应的值的，比如-1%5=4  
* 但是因为不同语言定义负数取余是不一样的，所以要自己转化
* =》有的是 -1/5 = -1余4，有的是-1/5 = 0余-1
* =》-7/3 = -2余-1 或 -7/3 = -3余2 但是该题目我们要让他余2
* 时间复杂度O(n)
* 空间复杂度O(min(n,k)),当n<k时，最多n个和，当n>=k时，最多k个，因为取余了
*/
class Solution {
    public int subarraysDivByK(int[] A, int K) {
        Map<Integer,Integer> map = new HashMap<>();
        int sum = 0;
        int res = 0;
        //记录前缀和本身和K整除的情况（单个元素可以被k整除）
        map.put(0,1);
        for(int a:A){
            sum+=a;
            //这里对负数进行了转换，因为java负数取余时返回的是负数
            int key = (sum%K+K)%K;
            int same = map.getOrDefault(key,0);
            res+=same;
            map.put(key,same+1);
        }
        return res;
    }
}
```
