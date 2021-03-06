---
title: "算法-股票问题"
date: 2020-03-16T10:28:31+08:00
draft: true
---


# 算法-Best Time to Buy and Sell Stock II

[ Best Time to Buy and Sell Stock II](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/564/)

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

**Example 2:**

```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### 思路：

> 每个问题都可以用暴力的方式解决，如果解决不了，那就说明不够暴力。

- 方法一：可以遍历所有的情况，低买高卖，列出所有情况，然后把满足先买后卖再买入在卖的情况组合起来，计算分别获利多少，然后就可以进行比较取出最大值，就可以解答本题。
- 方法二：还有一个更简单的方法，我们可以每遇到低的就买，高了就卖，也就是比较连续两天，后一天是否比前一天价格更高，如果后一天>前一天,前一天就买入，后一天卖出，然后继续买入，卖出，这样就可以很简单的解决问题了。



方法二JS代码实现：

```js
var maxProfit = function(prices) {
    if(prices.length < 2){
        return 0
    }
    var lirun = 0
    for(var i = 1,j=0;i < prices.length;i++,j++){
      
        if( prices[i] > prices[j]){ 
            oneday = prices[i]-prices[j]
            lirun += oneday
        }
    }
    return lirun

};
```

