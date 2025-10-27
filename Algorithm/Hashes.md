# 哈希 Hash  
## 定义  
哈希算法（Hash Algorithm）是一种能将任意长度的输入数据，通过特定计算映射为固定长度输出的函数，其输出结果称为哈希值（Hash Value）或散列值。  

## 核心特性  
哈希算法的设计需满足以下关键特性，这些特性决定了其适用场景：
    输入敏感：输入数据的微小变化（如一个字符的修改），会导致输出的哈希值发生巨大改变，可用于校验数据完整性。
    固定输出：无论输入数据的长度是 1 字节还是 1GB，输出的哈希值长度固定（如 MD5 输出 128 位，SHA-256 输出 256 位），便于存储和比较。
    高效计算：对任意输入数据，能快速计算出对应的哈希值，即使数据量大，也能在毫秒级或秒级完成，适合高频次使用场景。
    抗碰撞性：
        弱抗碰撞：很难找到两个不同的输入，使其产生相同的哈希值。
        强抗碰撞：已知一个输入和其哈希值，很难找到另一个不同的输入，使其产生相同的哈希值。   

## 例题
### e.g.1 字母异位词分组
问题描述：给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。
示例 1:

输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]

输出: [["bat"],["nat","tan"],["ate","eat","tea"]]

解释：

在 strs 中没有字符串可以通过重新排列来形成 "bat"。
字符串 "nat" 和 "tan" 是字母异位词，因为它们可以重新排列以形成彼此。
字符串 "ate" ，"eat" 和 "tea" 是字母异位词，因为它们可以重新排列以形成彼此。  

示例代码：  
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        //此处不是strs.length()，因为是字符串“数组”
        if (strs == null || strs.length == 0) {
            return null;
        }

        Map<String, Integer> strmap = new HashMap<>();
        List<List<String>> result = new ArrayList<>();
        int index = 0;

        for (String str : strs) {
            char[] chs = new char[str.length()];
            for (int i = 0; i < str.length(); i++) {
                chs[i] = str.charAt(i);
            }
            Arrays.sort(chs);
            String sortedStr = new String(chs);

            if (!strmap.containsKey(sortedStr)) {
                // 首次出现：创建新列表，存入 result，并记录索引
                strmap.put(sortedStr, index);
                result.add(new ArrayList<>()); // 初始化新列表
                result.get(index).add(str); // 向新列表添加元素
                index++;

            } else {
                result.get(strmap.get(sortedStr)).add(str);
            }
        }
        return result;

    }
}
```