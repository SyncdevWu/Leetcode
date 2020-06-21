
```
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。



上图为 8 皇后问题的一种解法。

给定一个整数 n，返回 n 皇后不同的解决方案的数量。

示例:

输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
 

提示：

皇后，是国际象棋中的棋子，意味着国王的妻子。皇后只做一件事，那就是“吃子”。当她遇见可以吃的棋子时，就迅速冲上去吃掉棋子。当然，她横、竖、斜都可走一或七步，可进可退。（引用自 百度百科 - 皇后 ）
```

```
class Solution {
    private int [] dx = new int [] {-1, -1, -1, 0, 0, 1 , 1 , 1};
    private int [] dy = new int [] {-1, 0, 1, -1, 1, -1 , 0 , 1};
    private int result = 0;
    public int totalNQueens(int n) {

        char [][] lines = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(lines[i], '.');
        }

        helper(lines, 0, n, new boolean[n][n]);
        return result;

    }

    private void helper(char [][] lines, int index, int n, boolean[][] visited) {
        if (index == n) {
            result++;
            return;
        }

        for (int i = 0; i < n; i++) {
            if (!visited[index][i]) {
                boolean [][] copy = new boolean [n][];
                for (int j = 0; j < n; j++) {
                    copy[j] = Arrays.copyOf(visited[j], n);
                }
                setVisited(visited, index, i, n);
                lines[index][i] = 'Q';
                helper(lines, index + 1, n, visited);
                lines[index][i] = '.';
                for (int j = 0; j < n; j++) {
                    visited[j] = Arrays.copyOf(copy[j], n);
                }
            }
        }
    }

    private void setVisited(boolean [][] visited, int x, int y, int n) {
        visited[x][y] = true;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < dx.length; j++) {
                int newX = x + dx[j] * i;
                int newY = y + dy[j] * i;
                if (newX >= 0 && newX < n && newY >= 0 && newY < n) {
                    visited[newX][newY] = true;
                }
            }
        }
    }
}
```
