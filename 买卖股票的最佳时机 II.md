# [买卖股票的最佳时机 II](https://leetcode-cn.com/leetbook/read/top-interview-questions-easy/x2zsx1/)[8.7]
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

```
示例 1:
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```
```
示例 2:
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
```
示例 3:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```
提示：
1 <= prices.length <= 3 * 10 ^ 4
0 <= prices[i] <= 10 ^ 4

# 首遍
我是又没有做出来，我是打算用昨天的双指针做，i代表波谷，j代表波峰。但是遇到的问题就是我想用双循环，把每一种可能遍历出来，但是遇到了不可知错误，就是出不来。我放弃了，看答案。之后可以看快一点。当作乐趣吧。

# 峰谷法
即判断每一个数字与后一个数字的关系，如果比它小就算作波谷，如果比它大，就算作波峰。每一次找到了波谷波峰就进行，将波峰-波谷值累加

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int i = 0;
        int valley = prices[0];
        int peak= prices[0];
        int maxProfit = 0;
        while(i< prices.size()-1){  //每次循环就是找到一次波峰波谷，进行一次累加
            while(i < prices.size()-1  && prices[i]>=prices[i+1]){
                i++;
            }
            valley = prices[i];   //找到波谷
            while(i < prices.size() -1 && prices[i] <= prices[i+1]){
                i++;
            }
            peak = prices[i];    //找到波峰
            maxProfit = maxProfit + peak -valley;    //计算差值并进行累加
        }
        return maxProfit;
    }
};
```

*时间复杂度：O(n)O(n)。遍历一次。
*空间复杂度：O(1)O(1)。需要常量的空间。

# 直接法
什么意思？就是仔细看题，股票可以当天买入当天卖出，意味着在理想的最佳收益中进行几次的插值都没有影响。我们只需要把所有的可能收益进行累加就可以了，完全不用管波峰波谷。这么简单我怎么没想到，有时候不要盲目解题，先看问题，仔细观察，寻找规律，抓住本质。

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxProfit=0;
        for (int i = 1; i< prices.size(); i++)
        {
            if(prices[i-1]<prices[i]){    \\如果后面一个数字大于前面一个数字，就是潜在收益
                maxProfit +=prices[i] -prices[i-1];   \\加！！！！
            }
        }
        return maxProfit;
    }
};
```
*时间复杂度：O(n)O(n)，遍历一次。
*空间复杂度：O(1)O(1)，需要常量的空间。
>足够直接了

# 所谓贪心（直接）法
和上面的直接法几乎一样，但是本质稍有不同。这里考虑的是，我们将股票的起伏看成一段一段的，凡是赚钱我们就进行买卖，赚钱。凡是亏钱，不买。

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxProfit=0;
        for (int i = 1; i< prices.size(); i++)
        {
            int tmp = prices[i]-prices[i-1];   //这里我先算一下未来的收益
            if(tmp >0) maxProfit +=tmp;   //如果赚钱就买卖，不赚钱就不买。
        }
        return maxProfit;
    }
};
```
*时间复杂度 O(N)O(N) ： 只需遍历一次price；
*空间复杂度 O(1)O(1) ： 变量使用常数额外空间。

>所以说和直接法几乎一样，但是思路不完全一样
