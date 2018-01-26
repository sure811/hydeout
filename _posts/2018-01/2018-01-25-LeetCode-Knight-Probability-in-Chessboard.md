---
layout: post
title: LeetCode - Knight Probability in Chessboard
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
On an NxN chessboard, a knight starts at the r-th row and c-th column and attempts to make exactly K moves. The rows and columns are 0 indexed, so the top-left square is (0, 0), and the bottom-right square is (N-1, N-1).

A chess knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.

Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

The knight continues moving until it has made exactly K moves or has moved off the chessboard. Return the probability that the knight remains on the board after it has stopped moving.
<!--more-->

Example:
```
Input: 3, 2, 0, 0
Output: 0.0625
Explanation: There are two moves (to (1,2), (2,1)) that will keep the knight on the board.
From each of those positions, there are also two moves that will keep the knight on the board.
The total probability the knight stays on the board is 0.0625.
```
Note:
* N will be between 1 and 25.
* K will be between 0 and 100.
* The knight always initially starts on the board.
### Java Solution
```java
class Solution {
    int[] x = new int[]{1, 2, 2, 1, -1, -2, -2, -1};
    int[] y = new int[]{-2, -1, 1, 2, -2, -1, 1, 2};
    public double knightProbability(int N, int K, int r, int c) {
        if(K == 0) return 1;
        double[][][] dp = new double[N][N][K + 1];
        for(int k = 0; k < K; k++){
            for(int i = 0; i < N; i++){
                for(int j = 0; j < N; j++){
                    if(k == 0) dp[i][j][0] = 1;
                    else{
                        for(int l = 0; l < x.length; l++){
                            if(i + x[l] >= 0 && i + x[l] < N && j + y[l] >= 0 && j + y[l] < N){
                                dp[i][j][k] += dp[i + x[l]][j + y[l]][k - 1] / 8;
                            }
                        }
                        // System.out.println(i + ":" + j + "|" + k + ":" + dp[i][j][k]);
                    }
                }
            }
        }
        for(int l = 0; l < x.length; l++){
            if(r + x[l] >= 0 && r + x[l] < N && c + y[l] >= 0 && c + y[l] < N){
                // System.out.println(r + x[l] + ":" + c + y[l] + ":" + dp[r + x[l]][c + y[l]][K - 1]);
                dp[r][c][K] += dp[r + x[l]][c + y[l]][K - 1];
            }
        }
        return dp[r][c][K] / 8;
    }
}
```