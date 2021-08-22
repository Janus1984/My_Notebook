[168. Excel表列名称 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/excel-sheet-column-title/)

给你一个整数 columnNumber ，返回它在 Excel 表中相对应的列名称。

例如：

A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...

``` python
class Solution:
    def convertToTitle(self, columnNumber: int) -> str:
        ans = list()
        while columnNumber-1 >= 0:
            a0 = (columnNumber - 1) % 26
            ans.append(chr(a0 + ord("A")))
            columnNumber = (columnNumber -1 - a0) // 26
        return "".join(ans[::-1])
```

* 26进制转换问题，只要x%26就是最后一位，(x-(x%26))%26就是倒数第二位，依次类推，直到x<0。
* 注意，这题的26进制是从1开始的，没有0，所以x始终要减一。
* chr()返回ASC码对应的字符，ord()返回字符对应的ASC码。