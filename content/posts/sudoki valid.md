---
title: "Valid Sudoku"
date: 2020-03-18T16:25:47+08:00
draft: true
---


# 算法-数独正确性检验（ Valid Sudoku）

### 原题目：

etermine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.



### 题意：

输入一个9*9的数独矩阵，判断这个数度矩阵设计是否符合规则，具体规则如下：

- 一行中1-9只能出现一次
- 一列中1-9只能出现一次
- 一个块中1-9只能出现一次（块指粗黑线的区域，也就是3*3的矩阵）



### 解题思路：

判断1所在的行，列，块三个是否有一个重合，如果有一个相同，那么就不符合规则。

遍历所有的数字，对每一个数字判断所在的行、列、块是否在之前这个数字的行、列、块中。

### 数据结构：

- hash表
- Set集合



### JS代码实现：

```js
/*
 * @lc app=leetcode.cn id=36 lang=javascript
 *
 * [36] 有效的数独
 */

// @lc code=start
/**
 * @param {character[][]} board
 * @return {boolean}
 */
/*
* 思路：每行、每列、每个块不能有重复的块，
*使用hash存储每个数字出现的行，列，块，
*如果一个数字出现相同的行 | 列 | 块则返回false
*/
var isValidSudoku = function (board) {
    // 输入：row，col
    // 输出：第几个方块 0-0 ~ 3-3
    function getBlock(row, col) {
        return `${Math.floor(row / 3)}-${Math.floor(col / 3)}`
    }

    function addNums(nums, row, col, block) {
        nums.rows.add(row)
        nums.cols.add(col)
        nums.blocks.add(block)
    }

  function newNums(){
    this.rows = new Set();
    this.cols = new Set();
    this.blocks = new Set();
  }

    let hashMap = {}
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[0].length; j++) {
            const current =  board[i][j]
            if (current !== '.') {
                const block = getBlock(i,j)
                if(hashMap[current]){
                    const hashCurrent = hashMap[current]
                    if(hashCurrent.cols.has(j)){return false}
                    // if(hashMap[current].cols.has(j)){return false}
                    if(hashCurrent.rows.has(i)){return false}
                    // if(hashMap[current].rows.has(i)){return false}
                    if(hashCurrent.blocks.has(block)){return false}
                    // if(hashMap[current].blocks.has(getBlock(i,j))){return false}
                }else{
                    hashMap[current] = new newNums()
                }
                addNums(hashMap[current],i,j,block)
            }
        }
    }
return true

};
// @lc code=end

```



