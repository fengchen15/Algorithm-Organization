# 回溯法 Backtracking Method
## 定义
回溯法（Backtracking）是一种通过试错探索所有可能解的算法思想，核心思路是：逐步构建解空间，当发现当前路径无法得到有效解时，退回上一步重新尝试其他选择（即 “回溯”），直到找到所有可行解或遍历完所有可能。
## 核心思想
想象走迷宫：从起点出发，每次选择一个方向前进；如果走到死胡同（无法到达终点），就退回上一个岔路口，选择另一个方向继续尝试。这个 “试错 - 退回 - 再试” 的过程，就是回溯法的核心。
## 用编程术语描述：
递归探索：通过递归逐步构建解（如组合、排列、路径等）。
剪枝（Pruning）：在递归过程中，若发现当前部分解已不可能形成有效解，立即停止该路径的探索，退回上一层。
回溯操作：尝试完一个选择后，撤销该选择（恢复现场），以便尝试其他选择。

## 例题
### e.g.1 括号生成  
问题描述：数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。  
解法：  

public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;
    }

    /**
     * 回溯生成有效括号组合
     * @param result 存储结果的集合
     * @param current 当前构建的字符串
     * @param open 已使用的左括号数量
     * @param close 已使用的右括号数量
     * @param max 最大括号对数（n）
     */
    private void backtrack(List<String> result, StringBuilder current, int open, int close, int max) {
        // 终止条件：字符串长度为 2n 时，生成一个有效组合
        if (current.length() == max * 2) {
            result.add(current.toString());
            return;
        }

        // 若左括号数量不足 n，可添加左括号
        if (open < max) {
            current.append('(');
            backtrack(result, current, open + 1, close, max);
            current.deleteCharAt(current.length() - 1); // 回溯：移除最后添加的左括号
        }

        // 若右括号数量小于左括号，可添加右括号（保证前缀有效）
        if (close < open) {
            current.append(')');
            backtrack(result, current, open, close + 1, max);
            current.deleteCharAt(current.length() - 1); // 回溯：移除最后添加的右括号
        }
